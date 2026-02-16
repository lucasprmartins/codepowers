---
name: brainstorm
description: Use quando o usuário tiver uma ideia ou conceito que ainda precisa ser refinado em especificação antes da implementação. Explora a intenção, requisitos e especificação por meio de diálogo colaborativo.
disable-model-invocation: true
user-invocable: true
argument-hint: [qual a descrição da task ou projeto?]
---

# Transformando Ideias em Projetos

## Visão Geral

Ajude a transformar a ideia do usuário em projetos e especificações completos por meio de um diálogo colaborativo natural:
```
$ARGUMENTS
```

Comece entendendo o contexto atual do projeto e, em seguida, faça perguntas uma de cada vez para refinar a ideia. Depois de entender o que você está construindo, apresente a especificação em pequenas seções (200 a 300 palavras), verificando após cada seção se está correta até o momento.

## O Processo

**Entendendo a ideia:**
- Se o input contiver URLs (Notion, Jira, etc.), busque o conteúdo usando as ferramentas MCP disponíveis antes de qualquer outra coisa
- Verifique o estado atual do projeto (arquivos, documentação, commits recentes)
- Faça perguntas uma de cada vez para refinar a ideia
- **OBRIGATÓRIO:** Use SEMPRE a ferramenta `AskUserQuestion` para fazer perguntas. Nunca faça perguntas em texto livre — use a interface interativa com opções clicáveis
- Apenas uma pergunta por mensagem - se um tópico precisar de mais exploração, divida-o em várias perguntas
- Concentre-se em entender: propósito, restrições, critérios de sucesso

**Explorando abordagens:**
- Proponha 2 a 3 abordagens diferentes com suas vantagens e desvantagens
- Use `AskUserQuestion` para apresentar as opções, com a recomendada como primeira opção (com sufixo "(Recomendado)")
- Comece com a opção recomendada e explique o porquê na descrição da opção

**Apresentando a especificação:**
- Assim que você acreditar que entendeu o que está construindo, apresente a especificação
- Divida-a em seções de 200 a 300 palavras
- Após cada seção, use `AskUserQuestion` para validar (ex: "Está correto?", "Ajustar algo?")
- Aborde: arquitetura, componentes, fluxo de dados, tratamento de erros
- Esteja preparado para voltar atrás e esclarecer se algo não fizer sentido

## Estrutura do Documento de Especificação

**Salvar especificações em:** `.codepowers/specs/AAAA-MM-DD-<tópico>.md`

**Todo documento de especificação DEVE seguir esta estrutura:**

```markdown
# Especificação: [Nome do Projeto/Funcionalidade]

> **Para Claude:** Este documento deve ser usado como entrada para a skill `codepowers:plan`.

**Objetivo:** [Uma frase descrevendo o que isso constrói]

**Contexto:** [2-3 frases sobre o problema que resolve]

## Requisitos Funcionais

- [Requisito 1]
- [Requisito 2]

## Arquitetura

**Abordagem:** [Descrição da abordagem escolhida e por que foi escolhida]

**Componentes:**
- [Componente 1]: [Responsabilidade]
- [Componente 2]: [Responsabilidade]

**Fluxo de Dados:** [Descrição do fluxo principal]

## Restrições e Decisões

- [Decisão técnica 1 e justificativa]
- [Restrição 1]

## Critérios de Sucesso

- [ ] [Critério verificável 1]
- [ ] [Critério verificável 2]
```

## Após a Especificação

**Implementação (se continuar):**
- Use `AskUserQuestion` para perguntar: "Pronto para configurar a implementação?" com opções "Sim, criar plano" e "Não, apenas salvar a especificação"
- Se sim: Use a habilidade `codepowers:plan` para criar um plano de implementação detalhado

## Princípios-chave

- **Uma pergunta por vez** - Não sobrecarregue com várias perguntas
- **Sempre use AskUserQuestion** - Toda pergunta deve usar a ferramenta interativa, nunca texto livre. O usuário deve poder clicar nas opções em vez de digitar
- **YAGNI implacavelmente** - Remova recursos desnecessários de todos os projetos
- **Explore alternativas** - Sempre proponha 2 a 3 abordagens antes de decidir
- **Validação incremental** - Apresente a especificação em seções e valide cada uma
- **Seja flexível** - Volte e esclareça quando algo não fizer sentido
