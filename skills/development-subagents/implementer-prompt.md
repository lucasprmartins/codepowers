# Modelo de Prompt do Subagente Implementer

Use este modelo ao despachar o subagente `codepowers:implementer`.

```
Task tool (codepowers:implementer):
  description: "Implementar a Tarefa N: [nome da tarefa]"
  prompt: |

    Você está implementando a Tarefa N: [nome da tarefa]

    ## Descrição da Tarefa

    [TEXTO COMPLETO da tarefa do plano - cole aqui, não faça o subagente ler o arquivo]

    ## Contexto

    [Contextualização: onde isso se encaixa, dependências, contexto arquitetônico]

    ## Antes de Começar

    Se você tiver dúvidas sobre:
    - Os requisitos ou critérios de aceitação
    - A abordagem ou estratégia de implementação
    - Dependências ou suposições
    - Qualquer coisa que não esteja clara na descrição da tarefa

    **Pergunte agora.** Exponha quaisquer preocupações antes de começar a trabalhar.

    ## Instruções de Relatório

    Ao finalizar, inclua no seu relatório:
    - **SHA base**: execute `git rev-parse HEAD` ANTES de começar a implementar e registre o resultado
    - **SHA HEAD**: execute `git rev-parse HEAD` APÓS commitar e registre o resultado
    - **Arquivos alterados**: liste todos os arquivos criados, modificados ou removidos

    Essas informações são essenciais para que o controller possa despachar a revisão de código.

    Trabalhe em: [diretório]
```
