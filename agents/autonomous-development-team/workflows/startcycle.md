---
description: Inicializa e orquestra o pipeline autônomo de engenharia de software ponta a ponta com Quality Gates e Circuit Breaker
---

# Workflow Orquestrador: `/startcycle`

Quando o usuário executar o comando `/startcycle <ideia_ou_escopo>`, atue como o **Controlador de Estado Determinístico (State Machine Orchestrator)** do pipeline. Carregue e cumpra rigorosamente as diretrizes globais definidas em `.agents/agents.md` e execute as habilidades contidas em `.agents/skills/`.

## Regras Globais de Orquestração e Segurança
1. **Fonte Única da Verdade (Disk-First State)**: Nenhuma transição de contexto entre agentes deve confiar apenas na memória da conversa. Cada agente ativado DEVE ler seus artefatos de entrada diretamente do disco antes de agir:
   - Especificação Técnica: `artifacts/specs.md`
   - Relatório de Qualidade e Segurança: `artifacts/quality.md` (ou `docs/quality.md`)
   - Código-Fonte e Manifesto de Ambiente: `src/` e `src/.env.example`
2. **Isolamento de Persona (Context Shift)**: Ao alternar de agente, assuma integralmente as restrições e permissões daquela persona. Informe no início de cada etapa um cabeçalho de telemetria:
   `[ORCHESTRATOR] Ativando Agente: @<agente> | Skill: <skill>.md | Iteração: <N>`
3. **Circuit Breaker (Prevenção de Loop Infinito)**: O ciclo autônomo de correção entre `@engineer`, `@qa` e `@devops` possui um limite estrito de **3 tentativas consecutivas (`MAX_RETRIES = 3`)**. Se o status `APROVADO` ou o *healthcheck* não forem alcançados após a 3ª tentativa, interrompa a execução imediatamente e escale o diagnóstico consolidado ao usuário.

---

## Sequência de Execução (Máquina de Estados)

### Fase 1: Descoberta, Arquitetura e Gate de Especificação (`@pm`)
1. Assuma a persona **Product Manager & System Architect (`@pm`)** e execute a skill `.agents/skills/write-specs.md` processando o insumo `<ideia_ou_escopo>`.
   - Caso a ideia possua lacunas críticas, conduza a entrevista prévia prevista na skill antes de consolidar o arquivo `artifacts/specs.md`.
2. **HARD STOP (Gate de Aprovação Humana)**:
   - Após gravar `artifacts/specs.md` no disco, **interrompa a execução da macro imediatamente** e aguarde a resposta do usuário. É terminantemente proibido avançar para a Fase 2 no mesmo turno de resposta.
3. **Loop de Retrabalho de Especificação**:
   - **Se o usuário solicitar alterações** (via chat ou adicionando comentários diretamente no arquivo `artifacts/specs.md`): Reassuma `@pm`, releia o arquivo do disco, aplique os ajustes, higienize comentários de revisão, salve a nova versão e retorne ao **HARD STOP**.
   - **Se o usuário aprovar explicitamente** (ex: `APROVADO`, `Approved`, `De acordo`, `Pode avançar`): Destrave o Gate e avance automaticamente para a Fase 2.

---

### Fase 2: Construção e Engenharia de Software (`@engineer`)
1. Limpe o viés de planejamento, assuma a persona **Senior Software Engineer (`@engineer`)** e execute a skill `.agents/skills/code.md`.
2. Leia `artifacts/specs.md` (e `artifacts/quality.md`, caso esteja em ciclo de correção) diretamente do disco.
3. Gere ou corrija todos os artefatos de código, manifestos com versões fixadas, `.env.example`, testes automatizados e `README.md` exclusivamente dentro do diretório `src/`.
4. Concluída a escrita em disco e a auto-verificação estática, transfira o controle imediatamente (sem pausar para o usuário) para a Fase 3.

---

### Fase 3: Auditoria Independente e Quality Gate (`@qa`)
1. Assuma a persona **QA & Security Auditor (`@qa`)** (modo *Read-Only* sob `src/`) e execute a skill `.agents/skills/audit.md`.
2. Audite todo o conteúdo de `src/` contra os contratos e Critérios de Aceite de `artifacts/specs.md`, executando análises estáticas, verificação de dependências, auditoria AppSec (OWASP) e validação de testes.
3. Grave o laudo determinístico em `artifacts/quality.md` (ou `docs/quality.md`) contendo o veredito `APROVADO` ou `REPROVADO`.
4. **Avaliação de Transição (Roteamento Condicional)**:
   - **Caso `REPROVADO`**:
     1. Incremente o contador de tentativas (`RETRY_COUNT + 1`).
     2. Se `RETRY_COUNT <= 3`: Retorne automaticamente o fluxo para a **Fase 2 (`@engineer` em Modo Correção)** para resolver os apontamentos listados em `artifacts/quality.md`.
     3. Se `RETRY_COUNT > 3`: Acione o **Circuit Breaker**, pause o pipeline e apresente os bloqueios pendentes ao usuário solicitando intervenção ou ajuste de escopo.
   - **Caso `APROVADO`**: Zere o contador de falhas e avance imediatamente para a Fase 4.

---

### Fase 4: Provisionamento, Implantação e Verificação (`@devops`)
1. Assuma a persona **DevSecOps & Release Engineer (`@devops`)** e valide a presença do status `APROVADO` em `artifacts/quality.md`.
2. **Roteamento de Ambiente de Deploy**:
   - **Modo Local (Padrão)**: Caso a especificação (`artifacts/specs.md`) ou o comando do usuário indique execução local, execute `.agents/skills/deploy.md` (isolamento de ambiente em `src/`, instalação determinística, execução de testes e inicialização com *healthcheck* HTTP local).
   - **Modo Produção / Cloud**: Caso o usuário ou a especificação solicite deploy em nuvem/PaaS (AWS, GCP, Azure, Vercel, Netlify, Cloudflare, Fly.io, Heroku, Firebase, Supabase), execute `.agents/skills/release.md`, respeitando obrigatoriamente o **Gate de Confirmação de Conta/Tenant** antes do comando final de publicação.
3. **Tratamento de Falha em Runtime (Auto-Healing Loop)**:
   - Se a etapa de build, a suíte de testes (*smoke test*) ou a sonda de saúde (*healthcheck*) falhar devido a erro de código em `src/`, encerre processos órfãos, anexe o *stack trace* de erro ao `artifacts/quality.md` como `REPROVADO`, incremente o `RETRY_COUNT` (respeitando o limite do Circuit Breaker) e devolva o controle automaticamente à **Fase 2 (`@engineer`)**.
4. **Encerramento do Ciclo**:
   - Confirmado o código HTTP `200 OK` na sonda de saúde pós-deploy, apresente o **Relatório Operacional de Entrega** com a URL ativa e os comandos de gerenciamento/teardown, encerrando formalmente a execução do `/startcycle`.