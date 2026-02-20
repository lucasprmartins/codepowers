---
name: finish
description: Use quando a implementação de alguma tarefa ou plano de desenvolvimento estiver completa apresentando opções estruturadas para finalização.
model: haiku
user-invocable: true
---

## Visão Geral

Guie a conclusão do trabalho de desenvolvimento apresentando opções claras e gerenciando o fluxo de trabalho escolhido.

**Princípio fundamental:** Verificar testes (se existirem) → Acionar agente de checagem.
**Anunciar no início:** "Estou usando a skill `finish` para concluir este trabalho. Vou seguir um processo estruturado para garantir que tudo esteja em ordem."

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

## Alertas

**Nunca:**
- Forçar push sem solicitação explícita
- Executar uma etapa que o usuário optou por pular

**Sempre:**
- Perguntar ao usuário antes de cada etapa se deseja executar ou pular

## Transferência

Após as verificações, use `AskUserQuestion` para perguntar se deseja criar a PR:

- **Pergunta:** "Verificações concluídas. Deseja criar a PR?"
- **Opção 1:** "Criar PR" — descrição: "Branch + push + PR em rascunho"
- **Opção 2:** "Parar por aqui" — descrição: "Encerrar sem criar PR"

**Se criar PR for escolhido:**

- Usar skill `codepowers:pr` para criação estruturada da PR
