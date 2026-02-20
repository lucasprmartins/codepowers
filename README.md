<div align="center">

<img src="https://cdn.simpleicons.org/claude" alt="Claude" width="80" />

# codepowers

**Skills, agentes e output styles para Claude Code — fluxo de desenvolvimento estruturado com subagentes paralelos.**

[Instalação](#instalação) · [Workflow](#workflow) · [Skills](#skills) · [Agentes](#agentes) · [Estrutura](#estrutura)

</div>

---

## Workflow

```
IDEIA → /brainstorm → /plan → /execute → /review → /finish → /pr
```

Cada skill faz seu trabalho e devolve o controle ao usuário via `AskUserQuestion`, criando gates de decisão entre etapas.

| Fase | Skill | O que faz |
|------|-------|-----------|
| **Brainstorming** | `/brainstorm` | Transforma ideia em especificação via diálogo interativo |
| **Planejamento** | `/plan` | Cria plano de implementação com tarefas granulares |
| **Execução** | `/execute` | Despacha implementers em fases paralelas |
| **Revisão** | `/review` | Revisão de código + checagem técnica + correções |
| **Finalização** | `/finish` | Testes → checagem |
| **Pull Request** | `/pr` | Branch + push + PR em rascunho |

### Execução em detalhe

```
/execute:
  Para cada fase de tarefas independentes:
    1. Despacha implementers em paralelo
       - Cada implementer: implementa, commita, reporta SHAs
       - NÃO faz review, lint, types ou build
    2. Aguarda e valida → próxima fase
  → AskUserQuestion: "Continuar para revisão?"

/review:
  1. Despacha codepowers:reviewer
     - Revisão de código (por tarefa ou diff geral)
     - Checagem técnica (lint, types, build)
  2. Se houver issues: despacha codepowers:fixer
  3. Verificação pós-fixer (lint/types/build)
  → AskUserQuestion: "Finalizar desenvolvimento?"

/finish:
  Testes → checagem
  → AskUserQuestion: "Criar PR?"

/pr:
  Branch + push + PR em rascunho
```

## Skills

| Skill | Modelo | Descrição |
|-------|--------|-----------|
| `/plan` | Opus | Plano de implementação detalhado com tarefas atômicas |
| `/brainstorm` | Sonnet | Refinamento de ideias em especificações via diálogo colaborativo |
| `/execute` | Sonnet | Orquestração de implementers paralelos por fase |
| `/review` | Sonnet | Revisão de código + checagem técnica + correções |
| `/design` | Sonnet | Criação de interfaces UI/UX profissionais |
| `/discussion` | Sonnet | Discussão técnica exploratória (método socrático) |
| `/commit` | Haiku | Commits atômicos agrupados por unidade lógica |
| `/pr` | Haiku | Branch + push + PR em uma operação |
| `/finish` | Haiku | Testes e checagem |

## Agentes

| Agente | Modelo | Função |
|--------|--------|--------|
| **implementer** | Sonnet | Implementa, commita e reporta SHAs |
| **reviewer** | Opus | Revisão de código + checagem técnica (lint/types/build) |
| **fixer** | Sonnet | Correções cirúrgicas de issues do reviewer |
| **checker** | Haiku | Verificação mecânica de lint, tipos e build |

### Distribuição de modelos

| Modelo | Papel |
|--------|-------|
| **Haiku** | Execução mecânica (lint, commits, PRs) |
| **Sonnet** | Produção de código e orquestração |
| **Opus** | Gates estratégicos (planejamento e revisão) |

## Estrutura

```
skills/
├── brainstorm/     # Refinamento de ideias
├── plan/           # Planejamento de implementação
├── execute/        # Orquestração de subagentes
│   ├── SKILL.md
│   └── implementer-prompt.md
├── review/         # Revisão de código + correções
│   ├── SKILL.md
│   ├── review-prompt.md
│   └── fixer-prompt.md
├── design/         # Criação de UI/UX
├── discussion/     # Discussão técnica
├── commit/         # Commits atômicos
├── pr/             # Criação de PRs
└── finish/         # Finalização

agents/
├── implementer.md  # Implementação de tarefas
├── reviewer.md     # Revisão de código
├── fixer.md        # Correção de issues
└── checker.md      # Lint, tipos e build

output-styles/      # Catálogo de posturas
```

## Output Styles

Posturas de comportamento ativadas via `/output-style [nome]`:

| Style | Descrição |
|-------|-----------|
| **critical** | Engenheiro sênior com pensamento crítico independente |
| **strict** | Guardião de convenções e padrões do projeto |
| **security** | Auditor de segurança com foco em OWASP e boas práticas |
| **mentor** | Mentor paciente que guia o raciocínio e explica o porquê |
| **pair** | Colega de pair programming colaborativo |
| **concise** | Executor direto com mínimo de ruído |
| **architect** | Arquiteto de software com visão sistêmica |

## Instalação

1. Adicione o marketplace:

```bash
/plugin marketplace add lucasprmartins/codepowers
```

2. Instale o plugin:

```bash
/plugin install codepowers@lucasprmartins/codepowers
```

3. Use as skills:

```bash
/codepowers:plan [especificação]
/codepowers:brainstorm [ideia]
/codepowers:commit
```

> Para testar localmente sem instalar: `claude --plugin-dir ./codepowers`

## Princípios

- **DRY** — código sem duplicação
- **YAGNI** — apenas o necessário
- **Commits frequentes** — atômicos e com mensagens claras
- **Revisão contínua** — detectar problemas cedo, antes que se alastrem
