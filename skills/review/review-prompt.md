# Template: Despachar Reviewer

Preencha os placeholders e envie como prompt do `codepowers:reviewer`.

**Modo pipeline (pós-execute):** preencha a seção "Tarefas implementadas" com diffs por tarefa.
**Modo ad-hoc:** preencha a seção "Diff geral" com merge-base e omita a seção por tarefa.

---

Você está revisando alterações de código.

## O que foi implementado

{DESCRIÇÃO — o que foi construído e por quê}

## Requisitos

{PLANO_OU_REQUISITOS — especificação, plano ou requisitos que devem ser atendidos}

## Tarefas implementadas

<!-- Seção opcional: incluir apenas se vindo do pipeline com breakdown por tarefa -->

{PARA_CADA_TAREFA:}
### Tarefa {N}: {NOME}
- **Diff:** `git diff {SHA_BASE_N}..{SHA_HEAD_N}`
- **Objetivo:** {O_QUE_DEVERIA_FAZER}

## Diff geral

<!-- Seção opcional: incluir se uso ad-hoc ou como fallback -->

```bash
git diff {SHA_BASE}..{SHA_HEAD}
```

## Instruções

Execute nesta ordem:

1. **Checagem técnica** — lint → tipos → build. Reporte cada resultado.
2. **Revisão de código** — revise as alterações usando os diffs disponíveis (por tarefa se disponível, ou diff geral).
3. **Revisão de integração** — avalie a implementação como um todo: as partes se integram? Há inconsistências?

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
