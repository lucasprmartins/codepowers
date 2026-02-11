# Codepowers

Plugin para Claude Code que adiciona skills, comandos e agentes especializados para melhorar o fluxo de trabalho de desenvolvimento de software.

## Fluxo de Trabalho

O codepowers organiza o desenvolvimento em fases sequenciais. Cada fase alimenta a seguinte:

```
IDEIA --> BRAINSTORMING --> PLANO --> EXECUÇÃO --> FINALIZAÇÃO
```

### Fase 1: Brainstorming (opcional)

**Comando:** `/brainstorming [descrição do projeto]`

Transforma uma ideia bruta em especificação completa por meio de diálogo colaborativo. O agente faz perguntas interativas (com opções clicáveis), explora 2-3 abordagens com prós/contras e apresenta a especificação em seções validadas incrementalmente.

**Saída:** `docs/spec/AAAA-MM-DD-<tema>.md`

Ao final, pergunta se deseja prosseguir para o planejamento.

### Fase 2: Planejamento

**Skill:** `write-plan` (acionada automaticamente pelo brainstorming ou manualmente)

Cria um plano de implementação detalhado com etapas granulares (2-5 minutos cada): implementar, verificar, commitar. O plano documenta arquivos exatos, código e comandos de verificação.

**Saída:** `docs/plans/AAAA-MM-DD-<feature>.md`

Ao final, oferece duas opções de execução:

| Opção | Quando usar | Como funciona |
|-------|-------------|---------------|
| **Subagentes (mesma sessão)** | Iteração rápida, tarefas independentes | Implementer por tarefa + revisão orquestrada pelo controller |
| **Sessão paralela** | Execução em lotes com checkpoints | Abrir nova sessão e executar `/execute-plan @arquivo` |

### Fase 3: Execução

#### Caminho A: Subagentes na mesma sessão

**Skill:** `development-subagents`

Para cada tarefa do plano, o controller orquestra o ciclo implementer → code-reviewer:

```
Para cada tarefa:
  1. Controller despacha codepowers:implementer com texto completo da tarefa
     - Pode fazer perguntas antes de começar
     - Implementa, verifica, commita, faz autoavaliação
     - Reporta com SHAs (base e HEAD) e arquivos alterados
  2. Controller despacha codepowers:code-reviewer com SHAs do relatório
     - Se issues críticos/importantes: despacha codepowers:fixer com issues
     - Repete revisão até aprovação
  3. Tarefa marcada como concluída

Após todas as tarefas:
  -> Revisão final de toda a implementação
  -> Aciona finish-dev
```

#### Caminho B: Sessão paralela

**Comando:** `/execute-plan [caminho do plano]`

Executa o plano em lotes de 3 tarefas com pontos de verificação:

```
1. Carrega e revisa o plano criticamente
2. Executa lote de 3 tarefas
3. Solicita revisão de código do lote
4. Gera relatório e aguarda feedback
5. Aplica ajustes -> próximo lote
6. Após todas as tarefas -> aciona finish-dev
```

### Fase 4: Finalização

**Skill:** `finish-dev` (acionada automaticamente pela execução)

Cada etapa é interativa — o usuário pode executar ou pular:

```
1. Verifica testes (se o projeto tiver) — executar ou pular
2. Aciona agente de checagem (lint, tipos, build) — executar ou pular
3. Push + criação da PR com título [TASK-XX] — executar ou pular
```

## Skills Utilitárias

Podem ser usadas a qualquer momento, independente do fluxo principal:

| Comando | O que faz |
|---------|-----------|
| `/commit` | Cria commits atômicos das alterações atuais, agrupando por unidade lógica |
| `/pr` | Cria branch + commit + checagem + push + PR em uma operação |
| `/ui-ux-design [o que criar]` | Cria interfaces UI/UX com estética profissional e distinta |

## Revisão de Código Sob Demanda

**Skill:** `request-code-review`

Pode ser acionada a qualquer momento para solicitar revisão de código:

- **Obrigatório:** após cada tarefa (subagentes), após cada lote (execute-plan), antes de merge
- **Opcional:** quando travado, antes de refatorar, após bug fix complexo

## Agentes

| Agente | Função | Acionado por |
|--------|--------|-------------|
| **implementer** | Implementa, commita e reporta com SHAs para revisão pelo controller | `development-subagents` |
| **fixer** | Corrige issues do code-reviewer com precisão cirúrgica | `development-subagents` |
| **code-reviewer** | Analista sênior: alinhamento com plano, qualidade, arquitetura, segurança | `request-code-review`, orquestrado pelo controller |
| **check** | Verificação de lint, tipos e build (detecta ecossistema: Node, Rust, Python, Go) | `finish-dev`, `/pr` |

## Princípios

- **DRY** (Don't Repeat Yourself) - Código sem duplicação
- **YAGNI** (You Ain't Gonna Need It) - Apenas o necessário
- **Commits frequentes** - Atômicos e com mensagens claras
- **Revisão contínua** - Detectar problemas cedo, antes que se alastrem

## Instalação

No Claude Code, execute o comando:

```
/plugin add https://github.com/lucasprmartins/codepowers
```

Para verificar se o plugin foi instalado corretamente:

```
/plugin list
```

## Autor

Lucas Martins (lucasprmartins@icloud.com)

## Repositório

https://github.com/lucasprmartins/codepowers
