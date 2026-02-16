---
name: review
description: Use ao concluir tarefas, implementar funcionalidades importantes ou antes de mesclar para verificar se o trabalho atende aos requisitos.
user-invocable: true
---

# Solicitar Revisão de Código

Acione o subagente codepowers:reviewer para detectar problemas antes que se alastrem.

**Princípio fundamental:** Revise cedo, revise com frequência.

## Quando Solicitar Revisão

**Obrigatório:**
- Após cada tarefa no desenvolvimento orientado por subagentes
- Após a conclusão de uma funcionalidade importante
- Antes da mesclagem com a branch principal

**Opcional, mas valioso:**
- Quando estiver travado (nova perspectiva)
- Antes de refatorar (verificação da linha de base)
- Após corrigir um bug complexo

## Como Solicitar

**1. Obtenha os SHAs do Git:**
```bash
BASE_SHA=$(git rev-parse HEAD~1) # ou origin/main
HEAD_SHA=$(git rev-parse HEAD)
```

**2. Acionar o subagente de revisão de código:**

Use a ferramenta Task com codepowers:reviewer e preencha o modelo em `code-review.md`

**Marcadores de posição:**
- `{O_QUE_FOI_IMPLEMENTADO}` - O que você acabou de construir
- `{PLANO_OU_REQUISITOS}` - O que deve fazer
- `{SHA_BASE}` - Commit inicial
- `{SHA_HEAD}` - Commit final
- `{DESCRIÇÃO}` - Breve resumo

**3. Agir com base no feedback:**
- Corrija problemas críticos imediatamente
- Corrija problemas importantes antes de prosseguir
- Anote problemas menores para depois
- Conteste se o revisor estiver errado (com justificativa)

## Exemplo

```
[Acabei de concluir a Tarefa 2: Adicionar função de verificação]

Você: Permita-me solicitar a revisão de código antes de prosseguir.

BASE_SHA=$(git log --oneline | grep "Task 1" | head -1 | awk '{print $1}')
HEAD_SHA=$(git rev-parse HEAD)

[Despacho codepowers:reviewer subagente]
  O QUE FOI IMPLEMENTADO: Funções de verificação e reparo para o índice de conversas
  PLANO OU REQUISITOS: Tarefa 2 de docs/plans/deployment-plan.md
  BASE_SHA: a7981ec
  HEAD_SHA: 3df7661
  DESCRIÇÃO: Adicionadas as funções verifyIndex() e repairIndex() com 4 tipos de problemas

[Retorno do subagente]:
  Pontos fortes: Arquitetura limpa, código bem organizado
  Problemas:
  Importante: Indicadores de progresso ausentes
  Menor: Número mágico (100) para o intervalo de relatório
  Avaliação: Pronto para prosseguir

Você: [Corrigir indicadores de progresso]
[Continuar para a Tarefa] 3]
```

## Integração com Fluxos de Trabalho

**Desenvolvimento Orientado a Subagentes:**
- Revisão após CADA tarefa
- Identificação de problemas antes que se agravem
- Correção antes de prosseguir para a próxima tarefa

**Execução de Planos:**
- Revisão após cada lote (3 tarefas)
- Obtenção de feedback, aplicação e continuidade

**Desenvolvimento Ad-Hoc:**
- Revisão antes da mesclagem
- Revisão em caso de travamento

## Sinais de Alerta

**Nunca:**
- Ignorar revisão por "ser simples"
- Ignorar problemas críticos
- Prosseguir com problemas importantes não corrigidos
- Discutir com feedback técnico válido

**Se o revisor estiver errado:**
- Contestar com argumentos técnicos
- Mostrar código/testes que comprovem o funcionamento
- Solicitar esclarecimentos

Veja o modelo em: review/code-review.md
