---
name: design
description: Crie interfaces de usuário e experiência de usuário distintas e de nível profissional com alta qualidade de design. Use esta habilidade quando o usuário solicitar a criação de componentes web, páginas, artefatos, pôsteres ou aplicativos (exemplos incluem sites, landing pages, dashboards, componentes React, layouts HTML/CSS ou ao estilizar/embelezar qualquer interface web). Gera código criativo e refinado e design de interface que evita a estética genérica de IA.
user-invocable: true
argument-hint: [o que deve ser criado?]
---

# UI/UX Design

Esta habilidade orienta a criação de UI/UX Design distintas e de nível profissional que evitam a estética genérica e artificial. Implemente código funcional com atenção excepcional aos detalhes estéticos e escolhas criativas.

Abaixo, o usuário forneceu os requisitos de UI/UX: um componente, página, aplicativo ou interface a ser construído. Ele pode ter incluído contexto sobre a finalidade, o público-alvo ou as restrições técnicas:
```
$ARGUMENTS
```

## Design Thinking

Antes de codificar, entenda o contexto e comprometa-se com uma direção estética ousada:
- **Propósito**: Qual problema esta interface resolve? Quem a utiliza?
- **Tom**: Escolha um extremo: brutalmente minimalista, caos maximalista, retrô-futurista, orgânico/natural, luxuoso/refinado, lúdico/brinquedo, editorial/revista, brutalista/cru, art déco/geométrico, suave/pastel, industrial/utilitário, etc. Há muitas opções para escolher. Use-as como inspiração, mas crie uma interface que seja fiel à direção estética escolhida.
- **Restrições**: Requisitos técnicos (framework, desempenho, acessibilidade).
- **Diferenciação**: O que torna isso INESQUECÍVEL? Qual é a única coisa que alguém vai se lembrar?
**CRÍTICO**: Escolha uma direção conceitual clara e execute-a com precisão. Maximalismo ousado e minimalismo refinado funcionam bem — a chave é a intencionalidade, não a intensidade.

Em seguida, implemente um código funcional (HTML/CSS/JS, React, Vue, etc.) que seja:
- Pronto para produção e funcional
- Visualmente impactante e memorável
- Coeso, com um ponto de vista estético claro
- Meticulosamente refinado em cada detalhe

## Diretrizes de Estética para Frontend

Foque em:
- **Tipografia**: Escolha fontes bonitas, únicas e interessantes. Evite fontes genéricas como Arial e Inter; opte por escolhas distintas que elevem a estética do frontend; escolhas de fontes inesperadas e cheias de personalidade. Combine uma fonte de exibição distinta com uma fonte de corpo refinada.
- **Cor e Tema**: Comprometa-se com uma estética coesa. Use variáveis CSS para consistência. Cores dominantes com acentos nítidos superam paletas tímidas e uniformemente distribuídas.
- **Movimento**: Use animações para efeitos e microinterações. Priorize soluções somente em CSS para HTML. Use a biblioteca Motion para React quando disponível. Concentre-se em momentos de alto impacto: um carregamento de página bem orquestrado com revelações escalonadas (animation-delay) cria mais encanto do que microinterações dispersas. Use estados de rolagem e de foco que surpreendam.
- **Composição Espacial**: Layouts inesperados. Assimetria. Sobreposição. Fluxo diagonal. Elementos que quebram a grade. Espaço negativo generoso OU densidade controlada.
- **Fundos e Detalhes Visuais**: Crie atmosfera e profundidade em vez de usar cores sólidas por padrão. Adicione efeitos contextuais e texturas que combinem com a estética geral. Aplique formas criativas como malhas de gradiente, texturas de ruído, padrões geométricos, transparências em camadas, sombras dramáticas, bordas decorativas, cursores personalizados e sobreposições de grãos.

JAMAIS utilize estéticas genéricas geradas por IA, como famílias de fontes batidas (Inter, Roboto, Arial, fontes do sistema), esquemas de cores clichês (principalmente gradientes roxos em fundos brancos), layouts e padrões de componentes previsíveis e designs padronizados que carecem de personalidade e contexto.

Interprete de forma criativa e faça escolhas inesperadas que pareçam genuinamente adequadas ao contexto. Nenhum design deve ser igual ao outro. Varie entre temas claros e escuros, fontes diferentes e estéticas diferentes. JAMAIS converja para escolhas comuns (Space Grotesk, por exemplo) em diferentes gerações.

**IMPORTANTE**: Adeque a complexidade da implementação à visão estética. Designs maximalistas exigem código elaborado com animações e efeitos complexos. Designs minimalistas ou refinados exigem contenção, precisão e atenção meticulosa ao espaçamento, tipografia e detalhes sutis. A elegância surge da execução impecável da visão.

Lembre-se: Claude é capaz de trabalhos criativos extraordinários. Não se reprima, mostre o que realmente pode ser criado quando se pensa fora da caixa e se compromete totalmente com uma visão singular.

## Regras

- Respeite sempre as diretrizes do projeto e da equipe.
- Verifique no projeto se já existe um padrão de temas estabelecido no CSS e não altere a não ser que o usuário tenha solicitado.
- Tenha coerência com o tema geral do projeto e os outros componentes.
