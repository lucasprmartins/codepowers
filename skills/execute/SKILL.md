---
name: execute
description: Utilize ao executar planos de implementação com tarefas independentes na sessão atual.
model: sonnet
user-invocable: true
argument-hint: [caminho do plano]
---

Execute o plano despachando subagentes `codepowers:implementer` em fases paralelas, agrupadas por dependências. Após todas as tarefas concluídas, despacha `codepowers:reviewer` para revisão com checagem técnica e `codepowers:fixer` para correções se necessário.

**Princípio fundamental**: Um bom plano é tão claro e detalhado que pode ser executado por um agente sem contexto adicional. A skill `execute` é responsável por seguir esse plano de forma estruturada, garantindo que as tarefas sejam concluídas corretamente, revisadas e corrigidas antes de finalizar.
**Anunciar no início:** "Estou usando a skill `execute` para executar um plano de implementação. Vou seguir um processo estruturado para garantir que as tarefas sejam concluídas corretamente e revisadas antes de finalizar."

## O Processo

```dot
digraph process {
    rankdir=TB;

    subgraph cluster_preparacao {
        label="1. Preparação";
        preparar [label="Ler plano\nExtrair tarefas com dependências\nRegistrar SHA base global\nCriar TodoWrite\nAgrupar em fases" shape=box];
    }

    subgraph cluster_fases {
        label="2. Implementação em Fases";
        despachar [label="Despachar implementers\nda fase em paralelo\n(múltiplas chamadas Task)" shape=box];
        aguardar [label="Aguardar TODOS\nconcluírem" shape=box];
        marcar [label="Marcar tarefas\ncomo concluídas" shape=box];
    }

    subgraph cluster_revisao {
        label="3. Revisão e Correção";
        reviewer [label="Despachar reviewer\n(review + lint/types/build)\n(./review-prompt.md)" shape=box];
        tem_issues [label="Issues\nencontrados?" shape=diamond];
        fixer [label="Despachar fixer\n(./fixer-prompt.md)" shape=box];
        verificar_fixer [label="Verificação pós-fixer\n(lint/types/build via Bash)" shape=box];
    }

    finish [label="4. Acionar\ncodepowers:finish" shape=box style=filled fillcolor=lightgreen];

    proxima [label="Próxima\nfase?" shape=diamond];

    preparar -> despachar;
    despachar -> aguardar;
    aguardar -> marcar;
    marcar -> proxima;
    proxima -> despachar [label="sim"];
    proxima -> reviewer [label="não\n(todas concluídas)"];
    reviewer -> tem_issues;
    tem_issues -> fixer [label="sim"];
    tem_issues -> finish [label="não"];
    fixer -> verificar_fixer;
    verificar_fixer -> finish;
}
```

## Preparação

1. Ler o arquivo do plano uma única vez
2. Extrair todas as tarefas com texto completo, contexto e dependências
3. Registrar SHA base global: `git rev-parse HEAD`
4. Criar TodoWrite com todas as tarefas
5. Agrupar tarefas em fases usando o campo `Depende de:`

## Agrupamento em Fases

O campo `Depende de:` de cada tarefa no plano determina o agrupamento:

1. Tarefas com `Depende de: Nenhuma` → **Fase 1**
2. Tarefas que dependem apenas de tarefas já concluídas → **próxima fase**
3. Dentro de uma fase: despachar **TODOS** os implementers simultaneamente (múltiplas chamadas Task na mesma mensagem)
4. Se uma fase tem apenas 1 tarefa, despachar normalmente

**Exemplo:**
- Tarefa 1: Nenhuma, Tarefa 2: Nenhuma, Tarefa 3: Tarefa 1, Tarefa 4: Nenhuma, Tarefa 5: Tarefa 3, Tarefa 4
- Fase 1: Tarefas 1, 2, 4 (paralelo) → Fase 2: Tarefa 3 → Fase 3: Tarefa 5

## Implementação por Fase

Para cada fase, na ordem:

1. Despachar implementers usando `./implementer-prompt.md` — fornecer texto completo da tarefa + contexto (nunca fazer o subagente ler o arquivo de plano)
2. Aguardar **TODOS** os implementers da fase concluírem
3. Marcar tarefas como concluídas, prosseguir para próxima fase

## Revisão e Correção

Após **todas** as fases concluídas:

1. Despachar `codepowers:reviewer` usando `./review-prompt.md` — checagem técnica (lint/types/build) + revisão particionada por tarefa + revisão de integração
2. Se houver issues: despachar `codepowers:fixer` usando `./fixer-prompt.md`
3. Verificação pós-fixer via Bash: lint → types → build
4. Acionar `codepowers:finish`

## Templates de Prompt

- `./implementer-prompt.md` — Despachar `codepowers:implementer`
- `./review-prompt.md` — Despachar `codepowers:reviewer`
- `./fixer-prompt.md` — Despachar `codepowers:fixer`

## Regras

**Nunca:**
- Fazer o implementer rodar lint, types, build ou review
- Despachar o reviewer antes de TODAS as tarefas estarem concluídas
- Despachar implementers de fases diferentes em paralelo
- Fazer o subagente ler o arquivo de plano (fornecer o texto completo)

**Sempre:**
- Aguardar TODOS os implementers de uma fase antes de prosseguir
- Fornecer texto completo + contexto ao implementer
- Registrar o SHA base global antes da primeira fase
- Verificar após o fixer (lint/types/build via Bash)

**Se o implementer fizer perguntas:**
- Responder de forma clara e completa
- Retomar o implementer com as respostas (via resume do subagente)

**Se o implementer falhar:**
- Re-despachar um novo implementer com instruções de correção específicas
- Não corrigir manualmente (poluição de contexto)
