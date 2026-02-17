# Template: Despachar Reviewer

Preencha os placeholders e envie como prompt do `codepowers:reviewer` após **TODAS** as tarefas concluídas.

---

Você está revisando a implementação completa de um plano.

## Tarefas implementadas

{PARA_CADA_TAREFA:}
### Tarefa {N}: {NOME}
- **Diff:** `git diff {SHA_BASE_N}..{SHA_HEAD_N}`
- **Objetivo:** {O_QUE_DEVERIA_FAZER}

## Plano original

{PLANO_OU_REQUISITOS — texto completo ou resumo relevante}

## Instruções

Execute nesta ordem:

1. **Checagem técnica** — lint → tipos → build. Reporte cada resultado.
2. **Revisão por tarefa** — revise cada tarefa usando o diff correspondente.
3. **Revisão de integração** — avalie a implementação como um todo: as tarefas se integram? Há inconsistências?

## Formato de saída

### Checagem Técnica
- **Lint:** passou/falhou [detalhes]
- **Tipos:** passou/falhou [detalhes]
- **Build:** passou/falhou [detalhes]

### Pontos Fortes
[O que foi bem feito]

### Issues

#### Crítico (Corrigir obrigatoriamente)
[Bugs, segurança, funcionalidades quebradas, falhas de checagem]

#### Importante (Corrigir)
[Arquitetura, funcionalidades ausentes, tratamento de erros]

#### Menor (Desejável)
[Estilo, otimizações]

Para cada issue: `arquivo:linha`, o que está errado, por que importa, como corrigir.

### Avaliação
**Pronto para prosseguir?** [Sim / Não / Com correções]
**Justificativa:** [1-2 frases]
