---
name: Implantação Segura em Produção Multi-Cloud e PaaS
description: Habilidade de implantação alternativa para levar o aplicativo direto para a produção em vez de apenas executá-lo localmente.
---

# Skill: Implantação Segura em Produção Multi-Cloud & PaaS (Deploy to Production)

## Objetivo
Atuar como Engenheiro de DevSecOps e Cloud Release (`@devops`) para empacotar, configurar e implantar a aplicação contida em `src/` em ambiente de produção remoto (AWS, GCP, Azure, Vercel, Netlify, Cloudflare, Fly.io, Railway, Heroku, DigitalOcean, Firebase ou Supabase), utilizando a CLI oficial autenticada localmente sob controles estritos de segurança, não interatividade e governança financeira (FinOps).

## Regras de Engajamento e Governança
- **Duplo Gate de Segurança (Qualidade + Confirmação de Tenant/Faturamento)**:
  1. **Gate de Qualidade**: Leia `docs/quality.md` (ou `artifacts/quality.md`). Se o arquivo não existir ou o status não for explicitamente `APROVADO`, aborte a operação imediatamente e retorne o fluxo ao `@qa` ou `@engineer`.
  2. **Gate de Destino**: Antes de executar o comando de publicação na nuvem, identifique o provedor, a conta ativa (*account/subscription/org*) e o projeto/região de destino. Se o usuário não tiver autorizado previamente o deploy naquele tenant específico, pause e solicite confirmação informando o identificador exato do destino.
- **Execução Estritamente Não Interativa**: Exporte `CI=true` no terminal e utilize obrigatoriamente flags de supressão de prompt (`--yes`, `--quiet`, `--non-interactive`, `--confirm`, `--no-wait`) para impedir bloqueios de execução (*stdin hangs*).
- **Isolamento de Segredos e Artefatos**:
  - É terminantemente proibido enviar arquivos `.env*` locais, diretórios `.git/`, `.venv/`, `node_modules/`, logs ou bancos de dados locais (`*.sqlite`, `*.db`) no pacote de upload da imagem ou bundle.
  - Segredos de produção devem ser injetados exclusivamente pelo cofre nativo da plataforma de destino via CLI, nunca embutidos no código-fonte em `src/` ou em manifestos versionados (`vercel.json`, `netlify.toml`, `wrangler.toml`, `fly.toml`, `Dockerfile`).
- **Prevenção contra Exaustão Financeira (FinOps)**: Sempre que o provedor suportar parâmetros de escala via CLI ou manifesto, configure limites conservadores de instâncias máximas, SKU básico, memória restrita e desativação de redundância desnecessária por padrão.

## Fluxo de Execução (Instruções Passo a Passo)

### Passo 1: Identificação de Plataforma e Verificação de Sessão (Auth Check)
1. Inspecione `artifacts/specs.md` para identificar o provedor de nuvem definido na arquitetura (ou detecte o provedor solicitado pelo usuário).
2. Verifique se a CLI correspondente está instalada e autenticada na máquina local executando o comando de inspeção de sessão da plataforma (conforme a Matriz de Provedores do Passo 4).
3. Caso a CLI não esteja instalada ou a sessão esteja expirada, interrompa o fluxo imediatamente e forneça ao usuário o comando exato de autenticação local.

### Passo 2: Higienização de Contexto e Adequação de Contrato em `src/`
Navegue até `src/` e aplique as regras de preparação conforme a topologia da plataforma:

1. **Geração de Arquivos de Exclusão (Ignore Files)**:
   - Crie ou atualize `.dockerignore`, `.gcloudignore`, `.vercelignore`, `.slugignore` ou `.gitignore` dentro de `src/` bloqueando: `.env`, `.env.*` (exceto `.env.example`), `.git/`, `.venv/`, `venv/`, `node_modules/`, `logs/`, `*.log`, `*.pid`, `*.sqlite`, `*.db`, `coverage/` e `.pytest_cache/`.
2. **Validação de Contrato de Execução por Topologia**:
   - **Containers & PaaS de Backend (AWS, GCP Cloud Run, Azure Container Apps/Web App, Fly.io, Railway, Heroku, DigitalOcean)**:
     - Confirme que o servidor lê a variável de ambiente `PORT` dinamicamente (com fallback para `8080` ou `3000`) e faz *bind* em `0.0.0.0` (nunca em `127.0.0.1` ou `localhost`).
     - Se baseado em container, garanta um `Dockerfile` otimizado (*multi-stage*) executando com **usuário não-root**. Se baseado em Buildpacks (Heroku/PaaS), valide a presença do `Procfile` ou script `start` no manifesto.
   - **Frontend Cloud, SSR & Edge (Vercel, Netlify, Cloudflare Pages/Workers, Azure Static Web Apps, Firebase)**:
     - Audite os arquivos em `src/` para garantir que nenhuma chave privada de servidor tenha recebido prefixos públicos de cliente (`NEXT_PUBLIC_`, `VITE_`, `REACT_APP_`, `PUBLIC_`).
     - Valide ou gere o manifesto de roteamento/build (`vercel.json`, `netlify.toml`, `wrangler.toml`, `firebase.json`, `staticwebapp.config.json`) apontando para o diretório de saída correto (ex: `.next`, `dist`, `build`).
   - **Backend-as-a-Service & Banco de Dados (Supabase)**:
     - Verifique se todas as tabelas nas migrações possuem *Row Level Security* (`ENABLE ROW LEVEL SECURITY`) ativado antes de aplicar `db push` no ambiente remoto.

### Passo 3: Build Local e Smoke Test Pré-Deploy
1. Execute a suíte de testes automatizados e o comando de compilação de produção localmente a partir de `src/`.
2. Se ocorrer qualquer erro de compilação, tipagem ou falha de teste, aborte o deploy imediatamente e retorne o controle ao `@engineer` (Modo Correção).

### Passo 4: Matriz de Deploy Não Interativo por Provedor
A partir do diretório `src/`, injete as variáveis de ambiente exigidas em `src/.env.example` e execute o deploy seguindo estritamente os parâmetros da plataforma alvo:

#### A. Hyperscalers (IaaS / Containers / Serverless)
- **Amazon Web Services (AWS)**:
  - *Auth Check*: `aws sts get-caller-identity --output json`
  - *Deploy (SAM / App Runner / Amplify)*: `sam deploy --no-confirm-changeset --no-fail-on-empty-changeset` ou atualização de serviço via `aws apprunner` / `aws ecs` com limites estritos de `MaxSize`, CPU e Memória.
  - *Logs*: `aws logs tail <LOG_GROUP> --since 10m`
- **Google Cloud Platform (GCP - Cloud Run)**:
  - *Auth Check*: `gcloud auth list --filter=status:ACTIVE --format="value(account)"` e `gcloud config get-value project`
  - *Deploy*: `gcloud run deploy <SERVICE> --source . --region=<REGION> --port=8080 --memory=512Mi --cpu=1 --min-instances=0 --max-instances=3 --timeout=60s --quiet`
  - *Logs / Teardown*: `gcloud run services logs read <SERVICE> --region=<REGION> --limit=50` | `gcloud run services delete <SERVICE> --region=<REGION> --quiet`
- **Microsoft Azure (Container Apps / App Service / Static Web Apps)**:
  - *Auth Check*: `az account show --query "{name:name, id:id, user:user.name}" --output json`
  - *Segredos / Config*: `az containerapp secret set -n <APP> -g <RG> --secrets <KEY>=<VAL>` ou `az webapp config appsettings set -n <APP> -g <RG> --settings <KEY>=<VAL>`
  - *Deploy (Container Apps)*: `az containerapp up --name <APP> --resource-group <RG> --location <LOCATION> --source . --ingress external --target-port 8080`
  - *Deploy (App Service)*: `az webapp up --name <APP> --resource-group <RG> --sku B1 --os-type Linux`
  - *Deploy (Static Web Apps)*: `npx @azure/static-web-apps-cli deploy <BUILD_DIR> --env production --app-name <APP>`
  - *Logs / Teardown*: `az containerapp logs show -n <APP> -g <RG> --tail 50` | `az group delete --name <RG> --yes --no-wait`

#### B. Frontend Cloud, Full-Stack Serverless & Edge
- **Vercel**:
  - *Auth Check*: `npx vercel whoami`
  - *Segredos*: `printf "%s" "$VALOR" | npx vercel env add <KEY> production`
  - *Deploy*: `CI=true npx vercel deploy --prod --yes`
  - *Logs / Teardown*: `npx vercel logs <DEPLOYMENT_URL>` | `npx vercel remove <PROJECT_NAME> --yes`
- **Netlify**:
  - *Auth Check*: `npx netlify status`
  - *Segredos*: `npx netlify env:set <KEY> "$VALOR"`
  - *Deploy*: `CI=true npx netlify deploy --prod --dir=<BUILD_DIR>`
  - *Logs / Teardown*: `npx netlify logs:function` | `npx netlify sites:delete <SITE_ID> --force`
- **Cloudflare (Workers & Pages)**:
  - *Auth Check*: `npx wrangler whoami`
  - *Segredos*: `printf "%s" "$VALOR" | npx wrangler secret put <KEY>`
  - *Deploy*: `CI=true npx wrangler deploy` (Workers) ou `CI=true npx wrangler pages deploy <BUILD_DIR> --project-name=<PROJECT>` (Pages)
  - *Logs / Teardown*: `npx wrangler tail` | `npx wrangler delete`

#### C. PaaS de Containers & Aplicações
- **Fly.io**:
  - *Auth Check*: `flyctl auth whoami`
  - *Segredos*: `flyctl secrets set <KEY>="$VALOR" --stage`
  - *Deploy (FinOps Single-Instance)*: `flyctl deploy --remote-only --ha=false --vm-memory 512 --yes`
  - *Logs / Teardown*: `flyctl logs --no-tail` | `flyctl apps destroy <APP_NAME> --yes`
- **Railway**:
  - *Auth Check*: `railway whoami` e `railway status`
  - *Segredos*: `railway variables set <KEY>="$VALOR"`
  - *Deploy*: `CI=true railway up --detach`
  - *Logs / Teardown*: `railway logs -n 50` | `railway down --yes`
- **Heroku**:
  - *Auth Check*: `heroku auth:whoami`
  - *Segredos*: `heroku config:set <KEY>="$VALOR" -a <APP_NAME>`
  - *Deploy & Escala*: Push do artefato de `src/` e trava de 1 dyno em `heroku ps:scale web=1 -a <APP_NAME>`
  - *Logs / Teardown*: `heroku logs -n 50 -a <APP_NAME>` | `heroku apps:destroy -a <APP_NAME> --confirm <APP_NAME>`
- **DigitalOcean App Platform**:
  - *Auth Check*: `doctl account get`
  - *Deploy*: `doctl apps create --spec .do/app.yaml` ou `doctl apps create-deployment <APP_ID> --wait`
  - *Logs / Teardown*: `doctl apps logs <APP_ID>` | `doctl apps delete <APP_ID> --force`

#### D. Backend-as-a-Service (BaaS)
- **Firebase (Hosting & Functions)**:
  - *Auth Check*: `npx firebase login:list`
  - *Deploy*: `CI=true npx firebase deploy --only hosting,functions --project <PROJECT_ID> --non-interactive`
  - *Logs / Teardown*: `npx firebase functions:log --project <PROJECT_ID>` | `npx firebase hosting:disable --project <PROJECT_ID> --confirm`
- **Supabase (Database & Edge Functions)**:
  - *Auth Check*: `npx supabase projects list`
  - *Segredos*: `npx supabase secrets set --env-file .env.production --project-ref <PROJECT_REF>`
  - *Deploy*: `npx supabase db push --project-ref <PROJECT_REF> && npx supabase functions deploy --project-ref <PROJECT_REF>`

### Passo 5: Sonda de Saúde Pós-Deploy (Post-Deploy Verification)
1. Extraia a URL pública oficial retornada pelo comando de deploy.
2. Aguarde a propagação inicial e execute uma verificação HTTP ativa (`curl -I -s -L -w "%{http_code}" <PRODUCTION_URL>/health` ou rota raiz) validando o código HTTP `200`.
3. Se o serviço retornar erro `5xx`, *timeout* ou falha de inicialização, execute imediatamente o comando de leitura de logs remotos da plataforma correspondente, identifique o *stack trace* e:
   - Se a falha for de configuração de variável de ambiente ou porta, corrija via CLI e reimplante.
   - Se a falha for bug de código em `src/`, reverta/suspenda o deploy e retorne o diagnóstico ao `@engineer` (Modo Correção).

### Passo 6: Relatório Operacional de Produção
Após confirmar o funcionamento da aplicação em produção via *healthcheck*, encerre sua execução apresentando exclusivamente o seguinte resumo técnico ao usuário:

```markdown
# Status de Implantação em Produção: ATIVO

- **Provedor / Plataforma**: [AWS | GCP | Azure | Vercel | Netlify | Cloudflare | Fly.io | Railway | Heroku | DigitalOcean | Firebase | Supabase]
- **Conta / Tenant / Projeto**: [Identificador exato validado na CLI]
- **Diretório Fonte**: `src/`
- **URL de Produção**: [URL HTTPS Oficial]
- **Status do Healthcheck**: [Código HTTP obtido]
- **Parâmetros de Escala / FinOps**: [Limites de instâncias, memória ou tier aplicados]

### Comandos de Governança, Diagnóstico e Rollback
- **Inspecionar logs de produção**: `<comando exato da CLI para leitura de logs>`
- **Suspender / Excluir recurso (Encerrar custos)**: `<comando exato da CLI para teardown/delete>`
```