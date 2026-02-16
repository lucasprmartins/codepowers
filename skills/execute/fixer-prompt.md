# Modelo de Prompt do Subagente Fixer

Use este modelo ao despachar o subagente `codepowers:fixer` para corrigir issues encontrados pelo reviewer.

```
Task tool (codepowers:fixer):
  description: "Corrigir issues da revisão da implementação completa"
  prompt: |

    Você está corrigindo issues encontrados na revisão de código da implementação completa.

    ## Issues para Corrigir

    [Lista de issues do reviewer — copiar output completo, incluindo issues de checagem técnica]

    ## Contexto

    [Resumo do que foi implementado, para o fixer entender o propósito do código]

    ## Instruções

    Corrija cada issue com precisão cirúrgica. Se um issue não fizer sentido, conteste com justificativa.

    **Proibições:** NÃO execute lint, types ou build. Apenas corrija os issues e commite.

    ## Relatório

    Ao finalizar, reporte:
    - **SHA base**: `git rev-parse HEAD` ANTES de corrigir
    - **SHA HEAD**: `git rev-parse HEAD` APÓS commitar
    - **Issues corrigidos**: lista com breve descrição do que foi feito
    - **Issues contestados**: quaisquer issues que não fazem sentido (com justificativa)

    Trabalhe em: [diretório]
```
