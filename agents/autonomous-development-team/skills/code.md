---
name: Engenharia e Geração de Código (Generate Code)
description: Essa habilidade é o criador principal. O agente de engenharia lê a pilha de tecnologia exata da especificação do gerente de projetos e cria dinamicamente todos os arquivos de código de front-end e back-end necessários.
---

# Skill: Engenharia e Geração de Código (Generate Code)

## Objetivo
Atuar como Engenheiro de Software Sênior (`@engineer`) para traduzir a Especificação Técnica aprovada (ou corrigir apontamentos do relatório de QA) em código-fonte completo, seguro, testável e pronto para produção dentro do diretório `src/`.

## Regras de Engajamento e Governança
- **Fidelidade Arquitetural Estrita**: Implemente o sistema utilizando exatamente a linguagem, versão, framework, arquitetura de pastas e contratos de dados definidos em `artifacts/specs.md` (ou `docs/spec.md`). Não introduza bibliotecas ou padrões arquiteturais não previstos sem justificativa técnica estrita.
- **Isolamento de Diretório (Sandbox)**: Todas as operações de escrita de arquivos devem ocorrer exclusivamente dentro do diretório `src/`. É proibido criar ou modificar arquivos fora deste escopo.
- **Proibição de Código Incompleto (Zero Placeholders)**: É estritamente proibido omitir blocos de código, usar comentários de truncamento (ex: `// ... resto do código`, `TODO:`, `FIXME:`, `pass` em funções produtivas) ou entregar implementações simuladas (*mocks* no lugar de lógica real). Todo arquivo gerado deve ser 100% funcional.
- **Segurança por Padrão (AppSec)**:
  - Nenhuma credencial, token, chave criptográfica ou string de conexão sensível deve constar no código-fonte. Utilize leitura de variáveis de ambiente e documente todas as chaves necessárias no arquivo `src/.env.example`.
  - Implemente validação e sanitização estrita em todas as fronteiras de entrada de dados (rotas HTTP, formulários, parâmetros de URL) e utilize consultas parametrizadas/ORMs para prevenir injeções (SQLi, XSS, Command Injection).

## Fluxo de Execução (Instruções Passo a Passo)

### Passo 1: Inspeção de Contexto e Modo de Operação
1. Leia integralmente o arquivo de especificação técnica (`artifacts/specs.md` ou `docs/spec.md`).
2. Verifique a existência de um relatório de auditoria prévio (`docs/quality.md`) ou logs de erro do `@devops`:
   - **Modo Criação (Greenfield)**: Se não houver relatório de falhas, inicie a construção completa seguindo a ordem topológica do Passo 2.
   - **Modo Correção (Bugfix/Refactor)**: Se houver um relatório com status `REPROVADO`, analise cada apontamento (arquivo, linha e causa raiz), aplique as correções cirúrgicas necessárias sem quebrar funcionalidades adjacentes e atualize os testes correspondentes.

### Passo 2: Construção em Ordem Topológica
Gere os arquivos dentro de `src/` respeitando a seguinte sequência de dependência para garantir integridade referencial:

1. **Configuração, Manifestos e Ambiente**:
   - Arquivos de dependências da stack com versões exatas fixadas (*pinned versions*, sem operadores de intervalo como `^` ou `~`): ex. `package.json`, `requirements.txt` / `pyproject.toml`, `.csproj`, `go.mod`.
   - Arquivos de configuração de compilação/linter (ex: `tsconfig.json`, `.eslintrc`, `appsettings.json`) e `.gitignore`.
   - Arquivo `.env.example` contendo todas as variáveis de ambiente exigidas pela especificação com valores de exemplo seguros.
2. **Camada de Domínio, Modelos e Contratos**:
   - Entidades, esquemas de banco de dados, migrações iniciais, DTOs (*Data Transfer Objects*) e interfaces/tipos compartilhados.
3. **Camada de Infraestrutura e Serviços (Backend)**:
   - Configuração de conexão com banco de dados, clientes de integração externa, middlewares de autenticação/autorização, tratamento global de exceções e *logging* estruturado.
   - Lógica de negócios (Services/Use Cases) aderente aos princípios SOLID e DRY.
4. **Camada de Apresentação e Rotas (API / Frontend)**:
   - Controladores, rotas de API com validação de payload e documentação/healthcheck (ex: rota `/health`).
   - Componentes de interface, gerenciamento de estado, integração com a API e tratamento visual de estados de carregamento (*loading*) e erro.
5. **Suíte de Testes Automatizados**:
   - Testes unitários e de integração cobrindo as regras de negócio, casos de borda e todos os Critérios de Aceite (Dado/Quando/Então) definidos na especificação.
6. **Documentação Operacional (`src/README.md`)**:
   - Instruções exatas e determinísticas de instalação, variáveis de ambiente necessárias, comando de execução dos testes e comando de inicialização do servidor para consumo direto pelo `@devops`.

### Passo 3: Auto-Verificação Estática (Self-Check)
Antes de encerrar sua execução e transferir o controle para o `@qa`, valide internamente:
- Todas as importações entre arquivos locais possuem caminhos relativos/absolutos corretos e os arquivos de destino existem em `src/`?
- Todos os pacotes externos importados no código estão explicitamente declarados no arquivo de manifesto (`package.json`, `requirements.txt`, etc.)?
- Todas as promessas/chamadas assíncronas possuem tratamento de erro adequado (`try/catch` ou equivalente)?

### Passo 4: Transferência de Controle (Handoff)
Conclua a geração informando de forma objetiva a árvore de arquivos criada/modificada em `src/` e sinalize que o artefato está pronto para a auditoria do agente `@qa`.