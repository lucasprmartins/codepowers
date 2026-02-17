---
name: finish
description: Use quando a implementação de alguma tarefa ou plano de desenvolvimento estiver completa apresentando opções estruturadas para finalização.
model: haiku
user-invocable: true
---

## Visão Geral

Guie a conclusão do trabalho de desenvolvimento apresentando opções claras e gerenciando o fluxo de trabalho escolhido.

**Princípio fundamental:** Verificar testes (se existirem) → Acionar agente de checagem → Enviar e criar PR.
**Anunciar no início:** "Estou usando a skill `finish` para concluir este trabalho. Vou seguir um processo estruturado para garantir que tudo esteja em ordem antes de criar a PR."

## O Processo

**Antes de cada etapa**, use `AskUserQuestion` para perguntar ao usuário se deseja executar ou pular aquela etapa. Respeite a escolha do usuário e prossiga para a próxima etapa caso ele opte por pular.

### Etapa 1: Verificar Testes

Pergunte: "Deseja executar os testes?" (opções: "Executar testes" / "Pular").

Se o usuário optar por executar:

- Verifique se o projeto possui testes configurados (ex: script `test` no `package.json`, diretório `tests/`, etc.).
- Se o projeto tiver testes, execute-os. Se falharem, corrija antes de prosseguir.
- Se o projeto não tiver testes, informe e prossiga.

```bash
# Execute o conjunto de testes do projeto (se existir)
bun test / cargo test / pytest / go test ./...
```

### Etapa 2: Acionar agente de checagem

Pergunte: "Deseja executar a checagem (lint, tipos e build)?" (opções: "Executar checagem" / "Pular").

Se o usuário optar por executar:

Execute o agente `codepowers:checker` para verificação de:
- Lint e formatação de código
- Tipos
- Build

**Prossiga após ele concluir a verificação.**

### Etapa 3: Enviar e Criar PR

Pergunte: "Deseja enviar a branch e criar a PR agora?" (opções: "Criar PR" / "Pular").

Se o usuário optar por criar:

**IMPORTANTE: A PR DEVE ser criada como rascunho (--draft). Nunca omita a flag --draft no comando `gh pr create`.**

```bash
# Enviar branch
git push -u origin <branch-de-recurso>
```

Use a ferramenta `AskUserQuestion` para perguntar ao usuário o ID da task relacionada a esta PR. Exemplo de pergunta: "Qual o ID da task relacionada a esta PR? (ex: 82)". Use o valor para compor o título no formato `<tipo>: <descrição> [TASK-<id>]`.

```bash
# Criar PR
gh pr create --draft --title "<tipo>: <descrição curta> [TASK-<id>]" --body "$(cat <<'EOF'
## Resumo
<descrição concisa do que foi feito e por quê>

## Alterações
- <alteração 1>
- <alteração 2>
- <alteração 3>

## Tipo de mudança
<!-- ignore-task-list-start -->
- [ ] Nova funcionalidade (feature)
- [ ] Correção de bug (bugfix)
- [ ] Refatoração (sem mudança de comportamento)
- [ ] Melhoria de performance
- [ ] Configuração / CI / Infra
<!-- ignore-task-list-end -->

## Verificação
- [ ] <etapas específicas para testar manualmente>

## Breaking changes
<descrever se houver mudanças que quebram compatibilidade, ou remover seção>
EOF
)"
```

## Alertas

**Nunca:**
- Forçar push sem solicitação explícita
- Executar uma etapa que o usuário optou por pular

**Sempre:**
- Perguntar ao usuário antes de cada etapa se deseja executar ou pular
