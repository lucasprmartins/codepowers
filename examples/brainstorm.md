# Exemplos de Input para `/brainstorm`

Abaixo estão 3 exemplos reais de como invocar a skill `brainstorm` em diferentes contextos de desenvolvimento.

---

## 1. Feature — Nova funcionalidade

```
/brainstorm Quero adicionar um sistema de notificações em tempo real no app. O usuário deve receber alertas quando alguém comenta em seu post ou quando é mencionado. Preciso decidir entre WebSockets e SSE, e como isso se integra com a arquitetura atual de microserviços.
```

---

## 2. Bug — Investigação e correção

```
/brainstorm Estamos com um bug intermitente onde o carrinho de compras perde itens depois que o usuário faz login. Acontece só em produção e não consigo reproduzir localmente. Quero fazer um brainstorm sobre possíveis causas (sessão, cache, race condition) e definir uma estratégia de investigação antes de sair mexendo no código.
```

---

## 3. Refactor — Reestruturação de código

```
/brainstorm O módulo de autenticação cresceu demais e virou um arquivo de 1200 linhas com lógica de login, registro, reset de senha, OAuth e validação de tokens tudo misturado. Quero refatorar isso em uma estrutura mais limpa sem quebrar nada. Preciso de ajuda para definir a separação de responsabilidades e a estratégia de migração incremental.
```
