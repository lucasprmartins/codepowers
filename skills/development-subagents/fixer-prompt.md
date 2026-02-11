# Modelo de Prompt do Subagente Fixer

Use este modelo ao despachar o subagente `codepowers:fixer` para corrigir issues encontrados pelo code-reviewer.

```
Task tool (codepowers:fixer):
  description: "Corrigir issues da revisão da Tarefa N: [nome da tarefa]"
  prompt: |

    Você está corrigindo issues encontrados na revisão de código.

    ## Issues para Corrigir

    [Lista de issues do code-reviewer — copiar output completo]

    ## Contexto

    [O que foi implementado, para o fixer entender o propósito do código]

    ## Instruções de Relatório

    Ao finalizar, inclua no seu relatório:
    - **SHA base**: execute `git rev-parse HEAD` ANTES de começar a corrigir e registre o resultado
    - **SHA HEAD**: execute `git rev-parse HEAD` APÓS commitar e registre o resultado
    - **Issues corrigidos**: liste cada issue endereçado e o que foi feito
    - **Issues contestados**: quaisquer issues que não fazem sentido (com justificativa)

    Essas informações são essenciais para que o controller possa despachar a re-revisão.

    Trabalhe em: [diretório]
```
