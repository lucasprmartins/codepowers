---
name: plan
description: Use quando você tiver uma especificação ou requisitos para uma tarefa de várias etapas, antes de mexer no código.
model: opus
user-invocable: true
argument-hint: [especificação ou requisitos]
---

## Visão Geral

Escreva planos de implementação abrangentes, assumindo que o engenheiro não tem nenhum contexto sobre nossa base de código. Documente tudo o que ele precisa saber: quais arquivos modificar para cada tarefa, código e documentação que ele possa precisar consultar. Apresente todo o plano em tarefas menores. Não repita código ou instruções entre tarefas. Inclua apenas o necessário — sem funcionalidades extras ou especulativas (DRY e YAGNI).

Assuma que ele é um desenvolvedor experiente, mas que não conhece quase nada sobre nosso conjunto de ferramentas ou domínio do problema.

**Princípio fundamental:** Um bom plano é tão claro e detalhado que pode ser executado por um agente sem contexto adicional. A skill `plan` é responsável por criar um plano que seja claro, detalhado e fácil de seguir, garantindo que todas as informações necessárias estejam incluídas para a execução bem-sucedida.
**Anunciar no início:** "Estou usando a skill `plan` para criar um plano de implementação. Vou seguir um processo estruturado para garantir que o plano seja claro, detalhado e fácil de seguir."
**Salvar planos em:** `.codepowers/plans/AAAA-MM-DD-<nome-da-funcionalidade>.md`

## Cabeçalho do Documento de Plano

**Todo plano DEVE começar com este cabeçalho:**

```markdown
# Plano de Implementação de [Nome da Funcionalidade]

> **Para Claude:** Este plano deve ser executado usando a skill `codepowers:execute`.

**Objetivo:** [Uma frase descrevendo o que isso constrói]

**Contexto:** [2-3 frases sobre o problema que resolve]

**Arquitetura:** [2-3 frases sobre a abordagem]

**Pilha de Tecnologias:** [Tecnologias/bibliotecas principais]
```

## Estrutura da Tarefa

```markdown
### Tarefa N: [Nome do Componente]

**Objetivo:** [Uma frase descrevendo o que esta tarefa entrega]

**Depende de:** Tarefa X, Tarefa Y (ou "Nenhuma")

**Arquivos:**

- Criar: `caminho/exato/para/arquivo.py`
- Modificar: `caminho/exato/para/arquivo.py existente:123-145`

**Implementação:**

def function(input):
return expected
```

**Sobre o campo `Depende de:`:**
- Obrigatório em todas as tarefas
- Usar "Nenhuma" para tarefas que podem ser executadas de forma independente
- Dependências determinam a ordem de execução por fases nos subagentes (tarefas independentes são executadas em paralelo)

## Lembre-se

- Sempre use caminhos de arquivo exatos
- Complete o código no plano (não use "adicionar validação")
- Referencie as funcionalidades relevantes com a sintaxe @
- DRY, YAGNI

## Transferência de Execução

Após salvar o plano, use `AskUserQuestion` para perguntar se deseja executar:

- **Pergunta:** "Plano salvo em `.codepowers/plans/<nome_do_arquivo>.md`. Deseja executar agora?"
- **Opção 1:** "Executar agora" — descrição: "Implementers paralelos por fase, revisão e checagem únicas após todas as tarefas"
- **Opção 2:** "Apenas salvar" — descrição: "Salvar o plano para executar depois"

**Se executar agora for escolhido:**

- Usar skill `codepowers:execute` para execução estruturada do plano
