# Template: Despachar Reviewer

Preencha os placeholders e envie como prompt do `codepowers:reviewer`.

**Modo pipeline (pós-execute):** preencha a seção "Tarefas implementadas" com diffs por tarefa.
**Modo ad-hoc:** preencha a seção "Diff geral" com merge-base e omita a seção por tarefa.

---

```markdown
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

**git diff {SHA_BASE}..{SHA_HEAD}**
```