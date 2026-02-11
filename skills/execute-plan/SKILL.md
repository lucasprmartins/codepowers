---
name: execute-plan
description: Utilize quando tiver um plano de implementação por escrito para executar em uma sessão separada com pontos de verificação de revisão.
disable-model-invocation: true
user-invocable: true
argument-hint: <docs/spec/arquivo-da-spec.md>
---

# Executando Planos

## Visão Geral

Carregar o plano, revisar criticamente, executar tarefas em lotes, gerar relatórios para revisão entre os lotes.

**Princípio fundamental:** Execução em lotes com pontos de verificação para revisão do arquiteto.

**Anunciar no início:** "Estou usando a habilidade de executar planos para implementar este plano."

## O Processo

### Etapa 1: Carregar e Revisar o Plano
1. Leia o arquivo do plano
2. Analise criticamente - identifique quaisquer dúvidas ou preocupações sobre o plano
3. Se houver preocupações: Discuta-as com seu parceiro humano antes de começar
4. Se não houver preocupações: Crie um TodoWrite e prossiga

### Etapa 2: Executar o Lote
**Padrão: Primeiras 3 tarefas**

Para cada tarefa:
1. Marque como em andamento
2. Siga cada etapa exatamente (o plano possui etapas pequenas)
3. Execute as verificações conforme especificado
4. Marque como concluída

### Etapa 3: Revisão de Código do Lote

Após concluir cada lote, solicite revisão de código:
- **SUBSKILL NECESSÁRIA:** Usar `codepowers:request-code-review`
- Revise as alterações do lote em relação ao plano
- Corrija problemas críticos e importantes antes de prosseguir
- Problemas menores podem ser anotados para depois

### Etapa 4: Relatório
Ao concluir o lote e a revisão:
- Mostre o que foi implementado
- Mostre o resultado da revisão de código
- Mostre a saída da verificação
- Diga: "Pronto para feedback."

### Etapa 5: Continuar
Com base no feedback:
- Aplique as alterações, se necessário
- Execute o próximo lote
- Repita até concluir

### Etapa 6: Concluir o Desenvolvimento

Após todas as tarefas serem concluídas e verificadas:
- **SUBSKILL NECESSÁRIA:** Usar `codepowers:finish-dev`.
- Anuncie: "Estou usando a skill finish-dev para concluir este trabalho."
- Use essa habilidade para acionar agente de checagem, enviar e criar PR.

## Quando parar e pedir ajuda

**PARE a execução imediatamente quando:**
- Encontrar um bloqueio no meio do processo (dependência ausente, teste falha, instrução pouco clara)
- O plano tiver lacunas críticas que impedem o início
- Você não entender uma instrução
- A verificação falhar repetidamente

**Peça esclarecimentos em vez de tentar adivinhar.**

## Quando revisar etapas anteriores

**Retorne à Revisão (Etapa 1) quando:**
- O parceiro atualizar o plano com base no seu feedback
- A abordagem fundamental precisar ser repensada

**Não force a resolução de bloqueios** - pare e pergunte.

## Lembre-se
- Analise o plano criticamente primeiro
- Siga os passos do plano exatamente
- Não ignore as verificações
- Consulte as habilidades quando o plano indicar
- Entre lotes: apenas relate e aguarde
- Pare quando estiver bloqueado, não tente adivinhar
- Nunca inicie a implementação na branch principal/master sem o consentimento explícito do usuário

## Integração

**Habilidades de fluxo de trabalho necessárias:**
- **codepowers:request-code-review** - Revisão de código após cada lote
- **codepowers:finish-dev** - Conclua o desenvolvimento após todas as tarefas
