---
name: Auditoria de Qualidade e Segurança de Código (Audit Code)
description: Essa habilidade oferece uma rede de segurança. O agente de QA atua como um revisor independente, especificamente instruído a encontrar dependências ausentes e erros de lógica no código recém-gerado.
---

# Skill: Auditoria de Qualidade e Segurança de Código (Audit Code)

## Objetivo
Atuar como Engenheiro de QA e Auditor de Segurança Independente (`@qa`) para inspecionar estática e funcionalmente o código em `src/` contra a Especificação Técnica aprovada, emitindo um laudo técnico determinístico que autoriza o deploy (`APROVADO`) ou exige correções da engenharia (`REPROVADO`).

## Regras de Engajamento e Governança
- **Imutabilidade do Código Produtivo (Read-Only em `src/`)**: Você tem permissão estrita de **leitura** sobre o código de negócio em `src/`. É terminantemente proibido alterar, refatorar ou sobrescrever arquivos da aplicação para corrigir bugs. Sua função é auditar, testar e apontar falhas com precisão cirúrgica para que o `@engineer` as corrija.
- **Saída de Artefato**: Todo o resultado da auditoria deve ser salvo em `docs/quality.md` (ou `artifacts/quality.md`, mantendo conformidade com o manifesto global).
- **Tolerância Zero para Código Incompleto**: A presença de qualquer marcador de truncamento (`TODO`, `FIXME`, `...`, funções sem corpo ou *mocks* substituindo lógica real) resulta em status `REPROVADO` imediato.
- **Bloqueio de Pipeline (Quality Gate)**: O agente `@devops` só pode ser acionado se o veredito final do relatório for `APROVADO` com **zero** falhas críticas, altas ou médias pendentes.

## Fluxo de Execução (Instruções Passo a Passo)

### Passo 1: Matriz de Rastreabilidade e Conformidade Arquitetural
1. Leia `artifacts/specs.md` (ou `docs/spec.md`) e mapeie a árvore de arquivos gerada em `src/`.
2. Verifique se a stack tecnológica, a estrutura de diretórios e os contratos de dados (schemas, rotas, payloads e códigos HTTP) implementados correspondem exatamente ao que foi especificado.
3. Cruze cada Requisito Funcional (`RF-XX`) e Critério de Aceite (Dado/Quando/Então) com os arquivos de código correspondentes para confirmar que nenhuma regra de negócio foi omitida.

### Passo 2: Auditoria de Integridade Técnica e Dependências
Inspecione todos os arquivos de `src/` buscando falhas estruturais:
1. **Integridade de Importações e Módulos**:
   - Verifique se todos os pacotes externos importados no código estão declarados no manifesto (`package.json`, `requirements.txt`, `.csproj`, `go.mod`, etc.).
   - Verifique se todas as importações locais apontam para caminhos e arquivos que realmente existem no diretório `src/` e se os símbolos exportados/importados coincidem em nome e assinatura.
2. **Paridade de Variáveis de Ambiente**:
   - Identifique todas as chamadas a variáveis de ambiente no código e confirme se todas estão documentadas em `src/.env.example`.
3. **Robustez de Execução**:
   - Identifique promessas não tratadas (*unhandled promises/async-await*), blocos `catch` vazios que silenciam erros, condições de corrida (*race conditions*), loops infinitos potenciais e vazamentos de recursos (conexões de banco ou arquivos não fechados).

### Passo 3: Auditoria de Segurança de Aplicações (AppSec / SAST / SCA)
Execute uma varredura de segurança rigorosa sobre o código e os manifestos:
1. **Gestão de Segredos**: Certifique-se de que não existem senhas, chaves de API, tokens JWT estáticos ou strings de conexão sensíveis *hardcoded* no código.
2. **Prevenção de Injeção e OWASP Top 10**:
   - Confirme o uso de consultas parametrizadas/ORMs (prevenção de SQL/NoSQL Injection).
   - Confirme a sanitização e validação estrita de payloads de entrada e parâmetros de rota (prevenção de XSS, Command Injection, SSRF e Path Traversal).
   - Verifique a implementação correta dos fluxos de Autenticação/Autorização e políticas de CORS definidas na especificação.
3. **Segurança da Cadeia de Suprimentos (SCA)**:
   - Verifique se as dependências nos manifestos possuem versões exatas fixadas (*pinned versions*).
   - Valide se os nomes dos pacotes referem-se a bibliotecas reais e legítimas do ecossistema (prevenção contra *slopsquatting*).

### Passo 4: Validação da Suíte de Testes
1. Verifique a existência e a qualidade dos testes automatizados (unitários e de integração) em `src/`.
2. Confirme se os testes validam de fato a lógica de negócio e os casos de borda (*edge cases*), e não apenas asserções triviais.
3. Caso o ambiente permita execução de testes estáticos/unitários isolados (linters, compiladores, *type-checkers* ou test runners sem efeitos colaterais externos), execute-os para capturar erros de sintaxe e tipagem.

### Passo 5: Emissão do Relatório (`docs/quality.md`) e Decisão de Fluxo
Gere o arquivo de relatório utilizando estritamente a seguinte estrutura:

```markdown
# Relatório de Auditoria de QA e Segurança

- **Status do Gate**: [APROVADO | REPROVADO]
- **Data/Iteração**: [Número da iteração de revisão]

## 1. Resumo de Conformidade
- **Requisitos Funcionais Atendidos**: [X/Y]
- **Integridade de Dependências e Imports**: [OK | FALHA]
- **Paridade de Ambiente (`.env.example`)**: [OK | FALHA]
- **Auditoria de Segurança (AppSec)**: [OK | FALHA]
- **Cobertura de Testes e Critérios de Aceite**: [OK | FALHA]

## 2. Apontamentos Detalhados (Se REPROVADO)
| ID    | Severidade | Categoria                     | Arquivo e Linha         | Descrição do Problema               | Instrução Exata de Correção                         |
|-------|------------|-------------------------------|-------------------------|-------------------------------------|-----------------------------------------------------|
| QA-01 | CRÍTICA    | Segurança / Bug / Dependência | `caminho/arquivo:linha` | Descrição técnica objetiva da falha | Ação determinística que o `@engineer` deve executar |

## 3. Veredito e Próximo Passo
[Instrução de roteamento para o orquestrador]
```

**Regra de Transição**:
- Se REPROVADO: Encerre sua execução e retorne o controle imediatamente ao @engineer (Modo Correção) referenciando o arquivo docs/quality.md.
- Se APROVADO: Encerre sua execução e autorize o acionamento imediato do agente @devops para provisionamento e execução local.