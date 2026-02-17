# Template: Despachar Reviewer (ad-hoc)

Preencha os placeholders e envie como prompt do `codepowers:reviewer`.

---

Você está revisando alterações de código.

## O que foi implementado

{DESCRIÇÃO — o que foi construído e por quê}

## Requisitos

{PLANO_OU_REQUISITOS — especificação, plano ou requisitos que devem ser atendidos}

## Diff

```bash
git diff {SHA_BASE}..{SHA_HEAD}
```

## Formato de saída

### Pontos Fortes
[O que foi bem feito]

### Issues

#### Crítico (Corrigir obrigatoriamente)
[Bugs, segurança, funcionalidades quebradas]

#### Importante (Corrigir)
[Arquitetura, funcionalidades ausentes, tratamento de erros]

#### Menor (Desejável)
[Estilo, otimizações]

Para cada issue: `arquivo:linha`, o que está errado, por que importa, como corrigir.

### Avaliação
**Pronto para prosseguir?** [Sim / Não / Com correções]
**Justificativa:** [1-2 frases]
