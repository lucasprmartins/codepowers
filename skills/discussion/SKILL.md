---
name: discussion
description: Use esta skill para conduzir discussões técnicas exploratórias sobre o projeto. Para entender código, tirar dúvidas, avaliar alternativas e estudar conceitos — sem implementação.
model: sonnet
user-invocable: true
argument-hint: [sua dúvida, ideia ou questão]
---

## Visão Geral

Conduza uma discussão técnica exploratória com o usuário. O objetivo é produzir **entendimento**, não código.

Input do usuário:
```
$ARGUMENTS
```

## Fases da Discussão

### 1. Explorar (2-3 interações)

Entenda o contexto antes de discutir:
- Se o input contiver URLs (Notion, Jira, docs, etc.), busque o conteúdo usando as ferramentas MCP disponíveis antes de qualquer outra coisa
- Explore o codebase para entender o estado atual do projeto (arquivos, arquitetura, documentação, commits recentes)
- Busque documentação externa relevante usando WebSearch, WebFetch ou MCPs de documentação (ex: Context7) quando necessário
- Use `AskUserQuestion` para entender o que o usuário quer explorar e o que já sabe

### 2. Aprofundar (3-5 interações)

Traga substância para a discussão:
- Apresente insights, comparações e trade-offs antes de perguntar
- Desafie premissas — questione o "por quê" por trás das escolhas
- Explore ângulos que o usuário não considerou
- Traga evidências do código real do projeto para fundamentar pontos
- Use `AskUserQuestion` quando precisar de input do usuário, não em toda mensagem
- Exemplos didáticos de código são permitidos para ilustrar conceitos, mas nunca gere código de implementação

### 3. Convergir (1-2 interações)

Sintetize e encerre:
- Resuma os principais pontos e conclusões da discussão
- Destaque decisões tomadas e questões que ficaram em aberto
- Use `AskUserQuestion` para perguntar: "Quer salvar um resumo desta discussão?"
  - Opções: "Sim, salvar resumo" / "Não, encerrar"
- Se sim: salve seguindo a estrutura abaixo

**Após ~5 interações com o usuário, comece a convergir ativamente.** Não prolongue a discussão indefinidamente.

## Estrutura do Documento de Discussão

**Salvar em:** `.codepowers/discussions/AAAA-MM-DD-<assunto>.md`

```markdown
# Discussão: [Assunto]

**Data:** [AAAA-MM-DD]
**Contexto:** [1-2 frases sobre o que motivou a discussão]

## Principais Insights
- [Insight 1]
- [Insight 2]

## Decisões
- [Decisão 1 e justificativa]

## Questões em Aberto
- [Questão 1]

## Referências
- [Arquivos, docs ou links relevantes consultados]
```

## Tipos de Discussão Suportados

- **Explorar código existente** — Entender como o projeto funciona, arquitetura, decisões de design, fluxo de dados
- **Dúvidas técnicas** — Documentação, APIs, bibliotecas, padrões de projeto, boas práticas
- **Avaliar alternativas** — Comparar abordagens, tecnologias, trade-offs sem compromisso de implementar
- **Estudo e aprendizado** — Aprofundar em conceitos, entender por que algo funciona de certa forma

## Guardrail: Limite com Implementação

Se a discussão evoluir naturalmente para algo implementável (ex: o usuário começar a definir requisitos, pedir especificações, ou querer transformar a discussão em ação), **não continue nessa direção**. Em vez disso:

- Use `AskUserQuestion` para sugerir a migração:
  - "Parece que essa discussão está evoluindo para algo implementável. Posso entrar em modo planejamento para planejar e implementar isso?"
  - Opções: "Sim, entrar em modo planejamento" / "Não, continuar discutindo"
- Se o usuário optar por continuar, respeite e mantenha o foco exploratório

## Princípios-chave

- **Insights antes de perguntas** — Sempre traga conteúdo substantivo antes de perguntar
- **AskUserQuestion quando precisar de input** — Use a ferramenta interativa para perguntas, mas não em toda mensagem
- **Embasamento real** — Fundamente no código do projeto e em documentação
- **Zero implementação** — Exemplos didáticos são OK, código de implementação não
- **Convergência ativa** — Após ~5 interações, sintetize e encerre
- **Guardrail ativo** — Se virar implementação, sugira entrar em modo planejamento
