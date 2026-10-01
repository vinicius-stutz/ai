---
title: Anatomia de uma Skill Perfeita
category: tips
target_model: Claude Code
---
# A Anatomia de uma Skill Perfeita
Princípios de arquitetura de skills, definição de escopo, regras e modularidade para agentes autônomos de IA.
## Estrutura de uma Skill Eficaz
Uma skill bem construída combina 5 elementos fundamentais:

| Elemento | Tipo | Descrição |
|----------|------|-----------|
| Definição de papel e expertise | **Papel** | Quem o agente é e qual é a sua especialização |
| Missão e resultado esperado | **Tarefa** | O que deve ser feito e qual o entregável final |
| Informações de contexto relevantes | **Contexto** | Dados que influenciam as decisões do agente |
| Justificativa do objetivo | **Raciocínio** | Por que esse resultado importa |
| O que deve ser entregue | **Entregáveis mínimos** | Critérios de aceitação claros |
| Formato da resposta esperada | **Saída** | Estrutura, formato e nível de detalhe esperado |
## Exemplo Completo

| Entrada | Tipo |
|---------|------|
| Você é um estrategista de conteúdo especializado em newsletters enxutas, mas com audiências altamente engajadas e leais. Seu foco é consistência e autenticidade, não volume. | **Papel** |
| Sua missão é criar um plano de conteúdo de 8 semanas para uma newsletter semanal sobre finanças pessoais, voltada para millennials. O resultado final deve ser um calendário pronto para execução. | **Tarefa** |
| Contexto do projeto:<br>- Newsletter sobre poupança e investimentos para pessoas entre 28 e 38 anos<br>- Produzida por uma única pessoa<br>- Sem orçamento para anúncios<br>- Atualmente com {{SUBSCRIBER_COUNT}} inscritos<br>- Principais desafios: cancelamentos, falta de diferenciação e inconsistência na publicação | **Contexto** |
| Objetivo: Parar de decidir temas de última hora e construir uma estratégia que aumente autoridade de forma consistente, com conteúdo relevante para o público. | **Raciocínio** |
| Requisitos do plano:<br>- 1 envio por semana durante 8 semanas<br>- Cada tema deve resolver ou prevenir um dos riscos citados<br>- Ao final, incluir 3 métricas claras para avaliar desempenho | **Entregáveis mínimos** |
| Para cada semana, entregue:<br>- Tema central<br>- Tipo de conteúdo (educativo, inspirador ou prático)<br>- Problema que o conteúdo resolve<br>- Sugestão de assunto para o email | **Saída** |
## Variáveis

| Variável | Descrição |
|----------|-----------|
| `{{SUBSCRIBER_COUNT}}` | Número atual de inscritos na newsletter |
## Boas Práticas
1. **Papel antes de tarefa**: Defina quem o agente é antes de dizer o que ele deve fazer.
2. **Contexto específico**: Quanto mais específico o contexto, mais personalizada a resposta.
3. **Entregáveis claros**: Especifique o que "feito" significa para evitar respostas incompletas.
4. **Formato de saída**: Indique se quer tabela, lista, markdown, JSON, etc.
5. **Raciocínio estratégico**: Explique o "por quê" para que o agente tome melhores decisões.
