---
name: review
description: Use ao concluir tarefas, implementar funcionalidades importantes ou antes de criar uma pull request verificando se o trabalho atende aos requisitos.
model: sonnet
user-invocable: true
---

# Revisão de Código

Acione o subagente `codepowers:reviewer` para detectar problemas antes que se alastrem. Pode ser usado a qualquer momento — dentro ou fora do fluxo de execução.

**Princípio fundamental:** A revisão de código é um passo crítico para garantir a qualidade do software. A skill `review` é responsável por solicitar uma revisão de código detalhada, permitindo que o revisor identifique problemas, forneça feedback e garanta que o trabalho atenda aos requisitos antes de prosseguir com a integração ou implantação.
**Anunciar no início:** "Estou usando a skill `review` para solicitar uma revisão de código."

## O Processo

**1. Obter SHAs:**
```bash
SHA_BASE=$(git merge-base HEAD origin/main) # ou HEAD~N para revisão parcial
SHA_HEAD=$(git rev-parse HEAD)
```

**2. Despachar `codepowers:reviewer`:**

Preencha o template em `./code-review.md` com:
- `{DESCRIÇÃO}` — o que foi implementado
- `{PLANO_OU_REQUISITOS}` — especificação ou requisitos
- `{SHA_BASE}` — commit base
- `{SHA_HEAD}` — commit final

**3. Agir sobre o feedback:**
- Críticos → corrigir imediatamente
- Importantes → corrigir antes de prosseguir
- Menores → anotar para depois
- Se o revisor estiver errado → contestar com argumentos técnicos

## Template

Veja o modelo em: `./code-review.md`

## Regras

**Nunca:**
- Ignorar problemas críticos
- Prosseguir com problemas importantes não corrigidos
- Discutir com feedback técnico válido

**Se o revisor estiver errado:**
- Contestar com argumentos técnicos
- Mostrar código/testes que comprovem o funcionamento
