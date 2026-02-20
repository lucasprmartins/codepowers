---
name: pr
description: Use para criar uma pull request.
model: haiku
user-invocable: true
allowed-tools: Bash
---

## Contexto

- Status atual do Git: !`git status`
- Diff atual do Git (alterações preparadas e não preparadas): !`git diff HEAD`
- Branch atual: !`git branch --show-current`

## Sua tarefa

Com base nas alterações acima:

1. Crie uma nova branch, se estiver na branch principal (main).
2. Crie um commit com uma mensagem apropriada.
3. Envie a branch para o repositório remoto.
4. Use a ferramenta `AskUserQuestion` para perguntar ao usuário o ID da task relacionada a esta PR. Exemplo de pergunta: "Qual o ID da task relacionada a esta PR? (ex: 82)". Use o valor para compor o título no formato `<tipo>: <descrição> [TASK-<id>]`.
5. Crie um pull request usando o formato abaixo. **IMPORTANTE: A PR DEVE ser criada como rascunho (--draft). Nunca omita a flag --draft no comando `gh pr create`.**

```bash
gh pr create --draft --title "<tipo>: <descrição curta> [TASK-<id>]" --body "$(cat <<'EOF'
## Resumo
<texto livre descrevendo o que foi feito e por quê>

## Alterações
- <alteração 1>
- <alteração 2>

## Critérios de Verificação
- [ ] <critério para o Tester verificar>
- [ ] <critério para o Tester verificar>

## Breaking changes
<descrever se houver mudanças que quebram compatibilidade, ou remover seção>
EOF
)"
```

6. Você tem a capacidade de chamar várias ferramentas em uma única resposta. Você DEVE fazer tudo isso em uma única mensagem. Não use nenhuma outra ferramenta nem faça nada além disso. Não envie nenhum outro texto ou mensagem além dessas chamadas de ferramentas.
