---
name: Provisionamento Seguro e Implantação Local (Deploy App)
description: Essa habilidade dá vida ao aplicativo. O agente do DevOps determina qual tipo de app foi criado (Node, Python etc.) e executa com segurança os comandos de terminal necessários para instalar módulos e iniciar o servidor.
---

# Skill: Provisionamento Seguro e Implantação Local (Deploy App)

## Objetivo
Atuar como Engenheiro de DevSecOps e Release (`@devops`) para validar o *Quality Gate* de auditoria, provisionar um ambiente de execução estritamente isolado, instalar dependências verificadas, executar migrações/testes e iniciar o servidor local da aplicação contida em `src/`, confirmando sua disponibilidade real via *healthcheck*.

## Regras de Engajamento e Governança
- **Verificação Obrigatória de Gate**: Antes de executar qualquer comando de terminal, leia `docs/quality.md` (ou `artifacts/quality.md`). Se o arquivo não existir ou o status não for explicitamente `APROVADO`, aborte a operação imediatamente e retorne o fluxo ao `@qa` ou `@engineer`.
- **Restrição Estrita de Privilégios (Hardening)**:
  - É terminantemente proibido executar comandos com `sudo`, `su` ou alterar permissões globais do sistema operacional (ex: `chmod 777`).
  - É proibido instalar pacotes de forma global no sistema hospedeiro (ex: `npm install -g`, `pip install` fora de um `venv`).
  - É proibido baixar e executar scripts remotos arbitrários via pipe (ex: `curl ... | bash` ou `wget ... | sh`).
- **Isolamento de Escopo**: Todos os artefatos de ambiente virtual, bancos de dados locais (ex: SQLite), arquivos `.env`, logs de execução e arquivos de PID devem residir estritamente dentro do diretório `src/`.
- **Imutabilidade de Código**: O `@devops` NÃO altera código-fonte de negócio para forçar a aplicação a subir. Se ocorrer erro de compilação ou falha de execução (*runtime crash*) decorrente do código, encerre os processos iniciados, colete o *stack trace* e devolva o fluxo ao `@engineer` (Modo Correção).

## Fluxo de Execução (Instruções Passo a Passo)

### Passo 1: Validação de Gate e Detecção Determinística da Stack
1. Confirme o status `APROVADO` no relatório de QA.
2. Inspecione `artifacts/specs.md` (ou `docs/spec.md`), `src/README.md` e os manifestos presentes em `src/` (`package.json`, `requirements.txt`, `pyproject.toml`, `.csproj`, `go.mod`) para identificar a versão exata da linguagem, o gerenciador de pacotes, a porta de rede configurada e os comandos de build, teste e inicialização.

### Passo 2: Preparação de Variáveis de Ambiente e Saneamento de Porta
1. **Provisionamento do `.env`**:
   - Verifique a existência de `src/.env.example`.
   - Caso `src/.env` ainda não exista, crie-o a partir do `.env.example`, preenchendo variáveis locais obrigatórias (ex: `PORT`, `DATABASE_URL` local, e gerando chaves efêmeras seguras para `JWT_SECRET` / `SECRET_KEY` quando aplicável).
2. **Verificação de Porta de Rede**:
   - Verifique se a porta definida para a aplicação está livre no host (utilizando comandos de diagnóstico de leitura como `lsof -i :<PORTA>` ou `ss -tulpn`).
   - Se a porta estiver ocupada por uma execução órfã anterior da própria aplicação em `src/`, encerre o processo antigo com segurança (via `kill <PID>`) antes de prosseguir; se estiver ocupada por um serviço externo do sistema, ajuste a variável `PORT` no arquivo `src/.env` para uma porta alta disponível (ex: `3001`, `8080`, `8000`).

### Passo 3: Isolamento e Instalação Determinística de Dependências
Navegue até `src/` e instale as dependências de acordo com a stack detectada, garantindo isolamento total:
- **Ecossistema Python**:
  1. Crie o ambiente virtual isolado: `python3 -m venv .venv`
  2. Instale os pacotes usando o binário local do ambiente virtual: `./.venv/bin/pip install --upgrade pip && ./.venv/bin/pip install -r requirements.txt`
- **Ecossistema Node.js / TypeScript**:
  1. Se houver `package-lock.json`, execute `npm ci --no-audit --no-fund`; caso contrário, execute `npm install --no-audit --no-fund`.
- **Ecossistema .NET / Go / Outros**:
  1. Execute os comandos nativos restritos ao diretório local (ex: `dotnet restore`, `go mod download`).
- **Migrações e Build**:
  1. Caso a especificação ou o `README.md` exija compilação prévia (ex: `npm run build`, `dotnet build`) ou migração de esquema de banco de dados (ex: Prisma, Alembic, Django Migrations, EF Core), execute-os nesta etapa e valide se o código de saída (*exit code*) é `0`.

### Passo 4: Execução da Suíte de Testes (Smoke Gate)
1. Execute o comando de testes automatizados definido no projeto (ex: `npm test`, `./.venv/bin/pytest`, `dotnet test`).
2. Se qualquer teste falhar, interrompa o deploy imediatamente, registre a saída de erro do terminal e retorne o controle ao `@engineer`.

### Passo 5: Inicialização em Background e Sonda de Saúde (Healthcheck)
1. Crie o diretório `src/logs/` (se não existir).
2. Inicie o servidor em *background* redirecionando a saída padrão (`stdout`) e a saída de erro (`stderr`) para `src/logs/server.log` e armazene o PID do processo em `src/.server.pid`.
   - *Exemplo*: `nohup <comando_de_start> > logs/server.log 2>&1 & echo $! > .server.pid`
3. **Verificação Ativa (Readiness Probe)**:
   - Aguarde de 2 a 5 segundos para a inicialização do runtime.
   - Verifique se o PID registrado em `.server.pid` continua em execução (`ps -p $(cat .server.pid)`).
   - Execute uma requisição HTTP local contra a rota de saúde ou rota raiz (ex: `curl -s -o /dev/null -w "%{http_code}" http://localhost:<PORTA>/health` ou `http://localhost:<PORTA>/`).
   - Se o processo tiver morrido ou retornar erro de servidor (`5xx` / conexão recusada), leia as últimas 50 linhas de `src/logs/server.log`, limpe o processo residual e devolva o diagnóstico exato ao `@engineer`.

### Passo 6: Relatório Operacional de Entrega
Após confirmar o retorno HTTP válido no *healthcheck*, encerre sua execução apresentando exclusivamente o seguinte resumo técnico ao usuário:

```markdown
# Status de Implantação Local: ATIVO

- **URL de Acesso**: http://localhost:<PORTA>
- **Endpoint de Healthcheck**: [Status HTTP obtido]
- **Stack / Runtime**: [Linguagem, Framework e Versão em execução]
- **PID do Servidor**: [Número do PID registrado em `src/.server.pid`]
- **Arquivo de Log**: `src/logs/server.log`

### Comandos de Gerenciamento Manual
- **Visualizar logs em tempo real**: `tail -f src/logs/server.log`
- **Encerrar o servidor com segurança**: `kill $(cat src/.server.pid) && rm src/.server.pid`
```