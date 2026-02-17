---
name: commit
description: Use essa skill para criar commits atômicos no git, agrupando alterações por unidade lógica.
model: haiku
user-invocable: true
allowed-tools: Bash(git status), Bash(git diff *), Bash(git branch *), Bash(git log *), Bash(git add *), Bash(git commit *)
---

## Contexto

- Status atual do Git: !`git status`
- Arquivos alterados (resumo): !`git diff HEAD --name-status`
- Diff completo: !`git diff HEAD`
- Branch atual: !`git branch --show-current`
- Commits recentes (para referência de estilo): !`git log --oneline -10`

## Sua tarefa

Crie commits atômicos no Git, agrupando as alterações por unidade lógica.

### Passo 1: Analisar e agrupar

Examine o diff e identifique grupos lógicos de alterações. Cada grupo deve representar UMA mudança coerente que possa ser descrita em uma única mensagem de commit.

**Critérios de agrupamento (em ordem de prioridade):**
1. Mesma funcionalidade ou correção (arquivos que juntos formam uma mudança coerente)
2. Mesmo tipo de alteração (feat, fix, refactor, docs, chore, test, style)
3. Na dúvida: se a mensagem de commit precisaria de "e" para conectar coisas não relacionadas, separe

**Quando NÃO separar:**
- Se todas as alterações são uma única unidade lógica, crie apenas um commit — não divida artificialmente
- Se um arquivo contém mudanças de dois grupos diferentes, inclua-o no grupo mais significativo (staging é por arquivo, não por trecho)

### Passo 2: Executar os commits

Para cada grupo, na ordem que mantenha o repositório válido a cada commit (dependências antes de dependentes):

1. `git add <arquivo1> <arquivo2> ...` — apenas os arquivos do grupo
2. `git commit -m "<tipo>: <descrição>"` — seguindo o estilo dos commits recentes

**Estilo da mensagem:** Use Conventional Commits em português, como nos commits recentes acima (feat:, fix:, refactor:, docs:, chore:, etc.). Mensagem curta e descritiva.

### Restrições

- Use `git add <arquivo>` para preparar arquivos (não use `git add -p` nem `git add -i`)
- Não use `git add .` nem `git add -A` — sempre especifique os arquivos
- Você tem a capacidade de chamar várias ferramentas em uma única resposta. Execute todos os commits necessários sem enviar texto ou mensagens adicionais
