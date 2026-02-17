# Codepowers

Plugin para Claude Code que adiciona skills, comandos e agentes especializados para melhorar o fluxo de trabalho de desenvolvimento de software.

## Fluxo de Trabalho

O codepowers organiza o desenvolvimento em fases sequenciais. Cada fase alimenta a seguinte:

```
IDEIA --> BRAINSTORMING --> PLANO --> EXECUÇÃO --> FINALIZAÇÃO
```

### Fase 1: Brainstorming (opcional)

**Comando:** `/brainstorm [descrição do projeto]`

Transforma uma ideia bruta em especificação completa por meio de diálogo colaborativo. O agente faz perguntas interativas (com opções clicáveis), explora 2-3 abordagens com prós/contras e apresenta a especificação em seções validadas incrementalmente.

**Saída:** `docs/spec/AAAA-MM-DD-<tema>.md`

Ao final, pergunta se deseja prosseguir para o planejamento.

### Fase 2: Planejamento

**Skill:** `plan` (acionada automaticamente pelo brainstorm ou manualmente)

Cria um plano de implementação detalhado com etapas granulares (2-5 minutos cada): implementar, verificar, commitar. O plano documenta arquivos exatos, código e comandos de verificação.

**Saída:** `docs/plans/AAAA-MM-DD-<feature>.md`

Ao final, pergunta se deseja executar o plano agora.

### Fase 3: Execução

**Skill:** `execute` (acionada automaticamente pelo plan)

O controller agrupa tarefas em ondas por dependências e despacha implementers em paralelo:

```
Para cada onda de tarefas independentes:
  1. Controller despacha implementers em paralelo
     - Cada implementer: implementa, commita, reporta SHAs
     - NÃO faz review, lint, types ou build
  2. Validação mecânica (lint/types via Bash)
  3. Aguarda e valida → próxima onda

Após TODAS as tarefas concluídas:
  4. Controller despacha codepowers:reviewer
     - Revisão de código particionada por tarefa
     - Checagem técnica (lint, types, build)
  5. Se houver issues: despacha codepowers:fixer
  6. Aciona finish
```

### Fase 4: Finalização

**Skill:** `finish` (acionada automaticamente pela execução)

Cada etapa é interativa — o usuário pode executar ou pular:

```
1. Verifica testes (se o projeto tiver) — executar ou pular
2. Aciona agente de checagem (lint, tipos, build) — executar ou pular
3. Push + criação da PR com título [TASK-XX] — executar ou pular
```

## Discussão Técnica

**Comando:** `/discussion [tema ou dúvida]`

Espaço de diálogo exploratório usando método socrático — sem implementação de código. Para entender o projeto, tirar dúvidas técnicas, avaliar alternativas e estudar conceitos. O Claude faz perguntas que guiam o raciocínio, desafia premissas e explora ângulos não considerados.

- Explora o codebase e busca documentação externa (web, MCPs) para embasar a discussão
- Se a discussão evoluir para algo implementável, sugere migrar para `/brainstorm`
- Ao final, oferece salvar um resumo opcional em `docs/discussions/`

## Skills Utilitárias

Podem ser usadas a qualquer momento, independente do fluxo principal:

| Comando | O que faz |
|---------|-----------|
| `/discussion [tema]` | Discussão técnica exploratória — entender código, dúvidas, alternativas, estudo |
| `/commit` | Cria commits atômicos das alterações atuais, agrupando por unidade lógica |
| `/pr` | Cria branch + commit + checagem + push + PR em uma operação |
| `/design [o que criar]` | Cria interfaces UI/UX com estética profissional e distinta |

## Revisão de Código Sob Demanda

**Skill:** `review`

Pode ser acionada a qualquer momento para solicitar revisão de código:

- **Obrigatório:** após todas as tarefas (subagentes), antes de merge
- **Opcional:** quando travado, antes de refatorar, após bug fix complexo

## Agentes

| Agente | Função | Acionado por |
|--------|--------|-------------|
| **implementer** | Implementa, commita e reporta com SHAs. Sem review ou checks. | `execute` |
| **fixer** | Corrige issues do reviewer com precisão cirúrgica. Sem checks. | `execute` |
| **reviewer** | Revisão de código + checagem de lint/types/build. Não edita código. | `review`, orquestrado pelo controller |
| **checker** | Verificação de lint, tipos e build (detecta ecossistema: Node, Rust, Python, Go) | `finish`, `/pr` |

## Output Styles

Posturas de comportamento que o Claude adota durante a sessão. Ative via `/output-style [nome]`:

| Style | Descrição |
|-------|-----------|
| **critical** | Engenheiro sênior com pensamento crítico independente |
| **strict** | Guardião de convenções e padrões do projeto |
| **security** | Auditor de segurança com foco em OWASP e boas práticas |
| **mentor** | Mentor paciente que guia o raciocínio e explica o porquê |
| **pair** | Colega de pair programming colaborativo |
| **concise** | Executor direto com mínimo de ruído |
| **architect** | Arquiteto de software com visão sistêmica |

## Princípios

- **DRY** (Don't Repeat Yourself) - Código sem duplicação
- **YAGNI** (You Ain't Gonna Need It) - Apenas o necessário
- **Commits frequentes** - Atômicos e com mensagens claras
- **Revisão contínua** - Detectar problemas cedo, antes que se alastrem