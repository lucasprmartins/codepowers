# Modelo de Prompt do Subagente Code-Reviewer

Use este modelo ao despachar o subagente `codepowers:reviewer` após **TODAS** as tarefas estarem concluídas.

```
Task tool (codepowers:reviewer):
  description: "Revisão de código e checagem técnica da implementação completa"
  prompt: |

    Você está revisando a implementação completa de um plano.

    ## O que foi implementado

    [RESUMO de todas as tarefas concluídas — nome e breve descrição de cada]

    ## Requisitos/Plano

    [PLANO ou requisitos originais — texto completo ou referência]

    ## Parte 1: Checagem técnica

    Identifique o ecossistema do projeto verificando os arquivos de configuração na raiz
    e execute as verificações na ordem: lint → tipos → build.

    Comandos comuns por ecossistema (adapte conforme o projeto):

    - Node.js/TypeScript (package.json): lint, check-types/tsc, build
    - Rust (Cargo.toml): cargo clippy, cargo check, cargo build
    - Python (pyproject.toml): ruff/flake8, mypy/pyright, python -m build
    - Go (go.mod): golangci-lint run, go vet, go build

    Reporte cada resultado: passou/falhou + erros específicos com arquivo:linha.

    ## Parte 2: Revisão de código (por tarefa)

    Revise cada tarefa individualmente usando o diff correspondente.

    [Para cada tarefa, incluir:]

    ### Tarefa N: [nome]
    - **Diff:** `git diff {SHA_BASE_N}..{SHA_HEAD_N}`
    - **Objetivo:** [o que a tarefa deveria fazer]

    Para cada tarefa, verifique:
    - Alinhamento com os requisitos (postura adversarial — não confie no relatório, leia o código)
    - Qualidade do código (erros, tipos, nomes, manutenibilidade)
    - Arquitetura (SOLID, acoplamento, integração)
    - Segurança e edge cases

    ## Parte 3: Revisão de integração

    Após revisar cada tarefa, avalie a implementação como um todo:
    - As tarefas se integram corretamente?
    - Há inconsistências entre tarefas (padrões diferentes, duplicação)?
    - O resultado final atende ao objetivo do plano?

    ## Formato de saída

    ### Checagem Técnica
    - **Lint:** passou/falhou [detalhes]
    - **Tipos:** passou/falhou [detalhes]
    - **Build:** passou/falhou [detalhes]

    ### Pontos Fortes
    [O que foi bem feito]

    ### Issues

    #### Crítico (Corrigir obrigatoriamente)
    [Bugs, segurança, perda de dados, funcionalidades quebradas, falhas de lint/types/build]

    #### Importante (Corrigir de bom grado)
    [Arquitetura, funcionalidades ausentes, tratamento de erros]

    #### Menor (Desejável)
    [Estilo, otimizações, documentação]

    Para cada issue: arquivo:linha, o que está errado, por que importa, como corrigir.

    ### Avaliação
    **Pronto para prosseguir?** [Sim / Não / Com correções]
    **Justificativa:** [1-2 frases]
```
