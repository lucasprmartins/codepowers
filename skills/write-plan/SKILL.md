---
name: write-plan
description: Use quando você tiver uma especificação ou requisitos para uma tarefa de várias etapas, antes de mexer no código.
---

# Planos de Escrita

## Visão Geral

Escreva planos de implementação abrangentes, assumindo que o engenheiro não tem nenhum contexto sobre nossa base de código e possui um gosto questionável. Documente tudo o que ele precisa saber: quais arquivos modificar para cada tarefa, código, documentação que ele possa precisar consultar e como verificar. Apresente todo o plano em tarefas menores. DRY (Don't Repeat Yourself - Não se Repita). YAGNI (You Ain't Gonna Need It - Você Não Vai Precisar Disso). Commits frequentes.

Assuma que ele é um desenvolvedor experiente, mas que não conhece quase nada sobre nosso conjunto de ferramentas ou domínio do problema.

**Avise no início:** "Estou usando a habilidade write-plans para criar o plano de implementação."

**Salvar planos em:** `docs/plans/AAAA-MM-DD-<nome-da-funcionalidade>.md`

## Granularidade de Tarefas em Etapas Contínuas

**Cada etapa corresponde a uma ação (2 a 5 minutos):**
- "Implementar a funcionalidade" - etapa
- "Verificar se funciona conforme esperado" - etapa
- "Confirmar" - etapa

## Cabeçalho do Documento de Plano

**Todo plano DEVE começar com este cabeçalho:**

```markdown
# Plano de Implementação de [Nome da Funcionalidade]

> **Para Claude:** Este plano deve ser executado usando uma das skills de execução do codepowers: `codepowers:development-subagents` (mesma sessão) ou `codepowers:execute-plan` (sessão paralela).

**Objetivo:** [Uma frase descrevendo o que isso constrói]

**Arquitetura:** [2-3 frases sobre a abordagem]

**Pilha de Tecnologias:** [Tecnologias/bibliotecas principais]
```

## Estrutura da Tarefa

```markdown
### Tarefa N: [Nome do Componente]

**Arquivos:**

- Criar: `caminho/exato/para/arquivo.py`
- Modificar: `caminho/exato/para/arquivo.py existente:123-145`

**Passo 1: Implementar a funcionalidade**

def function(input):
return expected

**Passo 2: Verificar se funciona**

Executar: `[comando de verificação relevante]`
Esperado: [resultado esperado]

**Passo 3: Confirmar o commit**

git add src/path/file.py
git commit -m "feat: adicionar funcionalidade específica"
```

## Lembre-se

- Sempre use caminhos de arquivo exatos
- Complete o código no plano (não use "adicionar validação")
- Use comandos exatos com a saída esperada
- Referencie as funcionalidades relevantes com a sintaxe @
- DRY, YAGNI, commits frequentes

## Transferência de Execução

Após salvar o plano, use `AskUserQuestion` para perguntar a abordagem de execução:

- **Pergunta:** "Plano salvo em `docs/plans/<nome_do_arquivo>.md`. Como deseja executar?"
- **Opção 1:** "Subagentes (esta sessão) (Recomendado)" — descrição: "Implementer autônomo por tarefa, com revisão de código interna e iteração rápida"
- **Opção 2:** "Sessão paralela (separada)" — descrição: "Abrir uma nova sessão do Claude Code e executar `/execute-plan @arquivo`"

**Se subagentes for escolhido:**

- **SKILL NECESSÁRIA:** Usar `codepowers:development-subagents`
- Permanecer nesta sessão
- Implementer autônomo por tarefa (implementa + revisão de código interna)

**Se sessão paralela for escolhida:**

- Orientá-los a abrir uma nova sessão no Claude Code.
