# Modelo de Prompt do Subagente Implementer

Use este modelo ao despachar o subagente `codepowers:implementer`.

```
Task tool (codepowers:implementer):
  description: "Implementar a Tarefa N: [nome da tarefa]"
  prompt: |

    Você está implementando a Tarefa N: [nome da tarefa]

    ## Descrição da Tarefa

    [TEXTO COMPLETO da tarefa do plano — cole aqui, não faça o subagente ler o arquivo]

    ## Contexto

    [Contextualização: onde isso se encaixa, dependências, contexto arquitetônico]

    ## Instruções

    Se tiver dúvidas sobre requisitos, abordagem ou dependências, pergunte antes de começar.

    **Proibições:** NÃO execute lint, types ou build. Apenas implemente e commite.

    ## Relatório

    Ao finalizar, reporte:
    - **SHA base**: `git rev-parse HEAD` ANTES de implementar
    - **SHA HEAD**: `git rev-parse HEAD` APÓS commitar
    - **Arquivos alterados**: lista dos arquivos criados/modificados/removidos
    - **Resumo**: 1-2 frases do que foi feito

    Trabalhe em: [diretório]
```
