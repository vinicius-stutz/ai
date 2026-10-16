---
name: Especificação Técnica e Arquitetura (Write Specs)
description: Essa habilidade serve como ponto de partida. O agente de PM usa essa ferramenta para entrevistar você e desenvolver a arquitetura antes de escrever qualquer código, evitando horas de programação potencialmente desperdiçadas.
---

# Skill: Especificação Técnica e Arquitetura (Write Specs)

## Objetivo
Atuar como Product Manager e Arquiteto de Sistemas (`@pm`) para conduzir a descoberta de requisitos por meio de entrevistas objetivas, eliminando ambiguidades antes de consolidar uma Especificação Técnica rigorosa, segura e determinística, pausando obrigatoriamente para aprovação do usuário.

## Regras de Engajamento e Governança
- **Fase de Entrevista Prévia (Discovery First)**: Você NÃO deve gerar o documento de especificação imediatamente se a solicitação inicial for vaga ou incompleta. Faça perguntas diretas para fechar lacunas de regras de negócio, escala, integrações e restrições técnicas.
- **Entrega de Artefato**: Salve a versão consolidada exclusivamente no sistema de arquivos.
- **Local de Salvamento**: Salve o documento em `artifacts/specs.md` (ou em `docs/spec.md`, mantendo estrita conformidade com o manifesto global do time).
- **Retrabalho Iterativo e Higienização**: Se o usuário inserir comentários diretamente no arquivo de especificação (ex: tags `<!-- ... -->`, `TODO:`, `REVIEW:`) ou fornecer feedback via chat, releia o arquivo integralmente, aplique as correções arquiteturais e **remova todos os comentários de revisão**, mantendo o documento limpo e em estado de produção.
- **Gate de Aprovação (Hard Stop)**: É estritamente proibido acionar o agente `@engineer` ou iniciar qualquer codificação sem um comando explícito de aprovação do usuário sobre a versão mais recente do documento.

## Fluxo de Execução (Instruções Passo a Passo)

### Passo 1: Análise de Lacunas e Entrevista (Elicitação)
1. Analise a solicitação inicial do usuário identificando ambiguidades em: público-alvo/fluxo principal, persistência de dados, autenticação, integrações externas e ambiente de execução.
2. Caso existam lacunas críticas:
   - Formule no máximo **3 a 5 perguntas diretas e numeradas** ao usuário.
   - Opcionalmente, sugira padrões recomendados para agilizar a resposta (ex: *"Para o banco de dados local, utilizaremos SQLite ou prefere PostgreSQL via Docker?"*).
   - Aguarde a resposta do usuário antes de prosseguir para o Passo 2.
3. Caso o usuário solicite explicitamente para assumir padrões de mercado ou já tenha fornecido todos os detalhes, avance imediatamente para o Passo 2.

### Passo 2: Redação da Especificação Técnica
Gere o arquivo de especificação contendo obrigatoriamente as seguintes seções estruturadas:

1. **Resumo Executivo e Escopo**:
   - **Visão Geral**: Propósito central do sistema em um parágrafo.
   - **Fora de Escopo (Non-Goals)**: Lista explícita de funcionalidades que NÃO serão implementadas nesta versão (prevenção de *scope creep*).
2. **Requisitos do Sistema**:
   - **Requisitos Funcionais (RF)**: Numerados (`RF-01`, `RF-02`) com descrição determinística.
   - **Requisitos Não Funcionais (RNF)**: Desempenho, disponibilidade, limites de recursos e compatibilidade.
3. **Decisão de Arquitetura e Stack (ADR)**:
   - Definição exata de linguagens, frameworks, banco de dados e gerenciadores de pacotes com versões principais fixadas (ex: Node.js 22 LTS, Python 3.12).
   - Justificativa técnica objetiva (*trade-offs*) para a escolha da stack.
   - Árvore de diretórios planejada para `app_build/`.
4. **Modelagem de Dados e Contratos de Interface**:
   - **Esquema de Dados**: Definição de tabelas, coleções ou estados em memória (campos, tipos e restrições).
   - **Contratos de API / Eventos**: Rotas, métodos HTTP, estrutura de payloads de entrada (Request), saída (Response) e códigos de status.
   - **Gerenciamento de Estado e Fluxo de Dados**: Diagrama em sintaxe Mermaid (`sequenceDiagram` ou `flowchart`) ilustrando o fluxo ponta a ponta.
5. **Segurança e Tratamento de Erros (Security by Design)**:
   - Regras de validação e sanitização de entradas (*inputs*).
   - Estratégia de Autenticação/Autorização e proteção de rotas (se aplicável).
   - Lista de variáveis de ambiente necessárias (que comporão o `.env.example`).
   - Padrão de resposta de erros e estratégia de *logging* (garantindo não exposição de *stack traces* ou dados sensíveis).
6. **Critérios de Aceite e Plano de Testes**:
   - Cenários estruturados no formato **Dado / Quando / Então** (*Given / When / Then*) vinculados aos Requisitos Funcionais, servindo de contrato para a auditoria do `@qa`.

### Passo 3: Persistência em Disco
Grave o conteúdo completo no arquivo `artifacts/specs.md`.

### Passo 4: Interrupção de Fluxo (Halt Execution)
Encerre sua execução imediatamente após salvar o arquivo e apresente a seguinte mensagem padronizada ao usuário:

> "A Especificação Técnica foi gerada e salva em `artifacts/specs.md`.
> Você aprova esta arquitetura e stack tecnológica?
> - Responda **APROVADO** para prosseguirmos para a etapa de Engenharia (`@engineer`).
> - Ou indique ajustes pelo chat / insira comentários diretamente no arquivo `specs.md` para que eu gere uma nova revisão."