# 🤖 Awesome AI Prompts & Skills
```
╔════════════════════════════════════════════════════════════════════════════════════════════════╗
║                                                                                                ║
║           █████╗ ██╗    ██╗███████╗███████╗ ██████╗ ███╗   ███╗███████╗   █████╗ ██╗           ║
║          ██╔══██╗██║    ██║██╔════╝██╔════╝██╔═══██╗████╗ ████║██╔════╝  ██╔══██╗██║           ║
║          ███████║██║ █╗ ██║█████╗  ███████╗██║   ██║██╔████╔██║█████╗    ███████║██║           ║
║          ██╔══██║██║███╗██║██╔══╝  ╚════██║██║   ██║██║╚██╔╝██║██╔══╝    ██╔══██║██║           ║
║          ██║  ██║╚███╔███╔╝███████╗███████║╚██████╔╝██║ ╚═╝ ██║███████╗  ██║  ██║██║           ║
║          ╚═╝  ╚═╝ ╚══╝╚══╝ ╚══════╝╚══════╝ ╚═════╝ ╚═╝     ╚═╝╚══════╝  ╚═╝  ╚═╝╚═╝           ║
║                                                                                                ║
║        ┌──────────────────────────────────────────────────────────────────────────────┐        ║
║        │                                                                              │        ║
║        │   >_ AWESOME AI PROMPTS & SKILLS                                             │        ║
║        │                                                                              │        ║
║        │   [ PROMPT ] ──► [ ◉ NEURAL CORE ◉ ] ──► [ SKILL ] ──► [ OUTPUT ]            │        ║
║        │                    ╱      │      ╲                                           │        ║
║        │                  0101    1010    1100                                        │        ║
║        │                    ╲      │      ╱                                           │        ║
║        │                     ╲─────┴─────╱                                            │        ║
║        │                       AI ENGINE                                              │        ║
║        │                                                                              │        ║
║        └──────────────────────────────────────────────────────────────────────────────┘        ║
║                                                                                                ║
║                 ░▒▓█  PROMPTS  •  SKILLS  •  WORKFLOWS  •  AUTOMATION  █▓▒░                    ║
║                                                                                                ║
╚════════════════════════════════════════════════════════════════════════════════════════════════╝
```

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md) [![PT-BR](https://img.shields.io/badge/lang-PT--BR-green)](README.md)

**Uma coleção cuidadosamente curada de prompts, skills, configurações e guias para potencializar seu uso de IAs generativas.** Não sabe do que se trata? [Saiba mais aqui](articles/ecossistema-de-ia.md).

*Exportado e higienizado a partir de notas reais do [Obsidian](https://obsidian.md/) - conteúdo testado no mundo real.*

[📚 Artigos](#-artigos) · [💬 Comandos Rápidos](#-comandos-rápidos) · [⚙️ Configurações](#%EF%B8%8F-configurações) · [💡 Dicas](#-dicas) · [💬 Prompts](#-prompts) · [🧠 Skills](#-skills) · [🤝 Contribuir](#-contribuindo)

## 🤔 Por que este repositório?
> [!NOTE]
> **Este repo é diferente!**
> A maioria dos repositórios de prompts é uma lista genérica e sem contexto.

Aqui você encontra **prompts com propósito**, organizados por objetivo real - não por ferramenta. Cada arquivo foi usado, refinado e validado na prática. Além de prompts, há **skills prontas** para agentes como Claude Code / Antigravity / Github Copilot, **configurações de comportamento** para personalizar IAs e **artigos** explicando como tudo funciona por baixo dos panos.

## 🗂️ Estrutura do Repositório
```
.
├── 📁 articles/             # Guias aprofundados sobre IA e agentes
├── 📁 commands/             # Comandos rápidos para LLMs no dia a dia
├── 📁 config/               # Configurações de comportamento para IAs
├── 📁 prompts/
│   ├── 🔍 analysis/         # Análise, pesquisa e tomada de decisão
│   ├── ⚡ automation/        # Automação de tarefas e rotinas
│   ├── 💼 career/           # Carreira e recolocação profissional
│   ├── 🚀 entrepreneurship/ # Empreendedorismo, marketing e vendas
│   ├── 💰 finance/          # Finanças pessoais e fluxo de caixa
│   ├── 🎨 image/            # Geração e edição de imagens
│   ├── 📚 learn/            # Aprendizado acelerado e estudos
│   ├── 🏢 management/       # Gestão de pessoas, tempo e reuniões
│   ├── 🧘 personal/         # Vida pessoal e produtividade
│   └── ✍️  text/            # Escrita, comunicação e copywriting
├── 📁 skills/               # Skills para Claude Code e agentes de IA
└── 📁 tips/                 # Dicas práticas de ferramentas e IA
```

## 📖 Como Usar
### Variáveis de Prompt
Todos os prompts com dados contextuais usam a convenção de **duplas chaves**:

```
{{NOME_DA_VARIAVEL}}
```

Basta substituir pelo seu contexto antes de usar. Ex: `{{SEU_SETOR}}` → `Tecnologia`.

### Frontmatter de Skills
Skills seguem o padrão de metadados YAML:

```yaml
---
name: "Nome da skill"
description: "O que ela faz em uma frase"
---

[corpo da skill em markdown...]
```

## 🗺️ Catálogo de IAs
Mapa rápido das principais IAs e suas especialidades:
- [Agentes autônomos](https://vinicius-stutz.raindrop.page/agentes-autonomos-74831742)
- [Assistentes de código](https://vinicius-stutz.raindrop.page/assistentes-de-codigo-74655258)
- [Clients de IA](https://vinicius-stutz.raindrop.page/clients-de-ia-74503440)
- [Criação de apresentações](https://vinicius-stutz.raindrop.page/apresentacao-63561579)
- [Estúdios de IA](https://vinicius-stutz.raindrop.page/estudios-de-ia-74503632)
- [Geração de imagens e vídeos](https://vinicius-stutz.raindrop.page/geracao-de-imagens-e-videos-54144539)
- [LLMs](https://vinicius-stutz.raindrop.page/llms-69382510)
- [Produção textual](https://vinicius-stutz.raindrop.page/producao-textual-54144289)
- [Runtimes e servidores](https://vinicius-stutz.raindrop.page/runtimes-e-servidores-74503558)
- [Síntese vocal e música](https://vinicius-stutz.raindrop.page/sintese-vocal-e-musica-74503433)

> [!TIP]
> **Saiba mais**
> Veja mais em uma [lista curada de repositórios comunitários](https://vinicius-stutz.raindrop.page/repositorios-comunitarios-74837396) sobre IA.

## 📚 Artigos
Guias completos para quem quer ir além do básico:
- [10 Passos para Construir Agentes do Zero](articles/10-passos-para-construir-agentes-do-zero.md) | Guia prático de construção de agentes de IA
- [Claude Code](articles/claude-code.md) | Guia prático sobre o uso do Claude Code
- [O Ecossistema de Inteligência Artificial](articles/ecossistema-de-ia.md) | Componentes e Estruturas de IA

## 💬 Comandos Rápidos
- [Comandos Rápidos do ChatGPT](commands/comandos-rapidos-do-chatgpt.md) | Atalhos e comandos para acelerar o uso do ChatGPT

## ⚙️ Configurações
Configurações de sistema para personalizar o comportamento das IAs:
- [Customização do Comportamento do ChatGPT](config/customizacao-do-comportamento-do-chatgpt.md) | Instruções de sistema para personalizar o ChatGPT
- [Instruções Customizadas para IA](config/instrucoes-customizadas-para-ia.md) | Template universal de instruções customizadas
- [Modo de Execução Objetiva do ChatGPT](config/modo-de-execucao-objetiva-do-chatgpt.md) | Configura o ChatGPT para respostas diretas e acionáveis

## 💡 Dicas
- [4 Passos para Gerar Conteúdos Convincentes](tips/4-passos-para-gerar-conteudos-convincentes.md) | Framework de persuasão aplicado à IA
- [8 Dicas de Engenharia de Prompt para Aprendizado](tips/8-dicas-de-prompts-de-engenharia-social-para-arrancar-o-potencial-maximo-da-ia-durante-o-aprendizado.md) | Extrai o máximo da IA nos estudos
- [A Anatomia de uma Skill Perfeita](tips/a-anatomia-de-uma-skill-perfeita.md) | Como estruturar skills eficazes para agentes
- [Claude - Como Usar](tips/claude-como-usar.md) | Introdução e melhores práticas do Claude
- [Claude Code - Como Usar](tips/claude-code-como-usar.md) | Guia completo do Claude Code em PT-BR
- [Claude Code - Skills Oficiais](tips/claude-code-skills-oficiais.md) | Catálogo das skills oficiais do Claude Code
- [Criação de Sites e Google Maps](tips/criacao-de-sites-e-google-maps.md) | Uso de IA para criação de presença digital e geolocalização
- [Crie Conteúdo para Instagram ou TikTok como um Preguiçoso](tips/crie-conteudo-para-o-instagram-ou-tiktok-como-um-preguicoso.md) | Produção de conteúdo para redes sociais com mínimo esforço
- [Deep Fake com Vídeos usando o Flow](tips/deep-fake-com-videos-usando-o-flow.md) | Técnicas de vídeo sintético com ferramentas acessíveis
- [Dicas Avançadas de IA](tips/dicas-avancadas-de-ia.md) | Técnicas avançadas para usuários experientes
- [Dicas para Melhorar Qualquer Prompt](tips/dicas-para-melhorar-qualquer-prompt.md) | Princípios universais de prompt engineering
- [Selfie com Celebridades com Kling e NanoBanana](tips/selfie-com-celebridades-com-kling-e-nanobanana.md) | Geração de fotos com figuras públicas usando IA
- [Usando IA no Dia a Dia Corporativo](tips/usando-ia-no-dia-a-dia-corporativo.md) | Casos de uso práticos no ambiente corporativo
- [YouTube Kids](tips/youtube-kids.md) | Dicas de uso seguro e produtivo do YouTube Kids com IA

## 💬 Prompts
### 🔍 Analysis - Análise e Decisão
- [5 Prompts Estratégicos para Análise Avançada de Conteúdo](prompts/analysis/5-prompts-estrategicos-para-analise-avancada-de-conteudo.md) | Framework completo de análise profunda de conteúdo
- [Assistente de Pesquisa](prompts/analysis/assistente-de-pesquisa.md) | Conduz pesquisas estruturadas como um analista sênior
- [Clareza de Pensamentos](prompts/analysis/clareza-de-pensamentos.md) | Organiza ideias difusas em raciocínio claro
- [Comparar Opções](prompts/analysis/comparar-opcoes.md) | Análise comparativa estruturada para tomada de decisão
- [Construa Modelos Mentais](prompts/analysis/construa-modelos-mentais.md) | Cria frameworks mentais para entender problemas complexos
- [Resolução de Problemas](prompts/analysis/resolucao-de-problemas.md) | Metodologia sistemática para resolver qualquer problema
- [Resolva Bloqueios Mentais](prompts/analysis/resolva-bloqueios-mentais.md) | Desbloqueie travamentos cognitivos e criativos
- [Resumo de Notas de CRM para Handoff](prompts/analysis/resumo-de-notas-de-crm-para-handoff.md) | Estrutura handoffs de CRM com clareza e contexto
- [Tomada de Decisões](prompts/analysis/tomada-de-decisoes.md) | Estrutura decisões complexas com critérios objetivos
- [Ultra Tempestade de Ideias](prompts/analysis/ultra-tempestade-de-ideias.md) | Geração massiva e diversificada de ideias

### ⚡ Automation - Automação
- [4 Prompts para Candidatar-se a 500 Vagas de Emprego](prompts/automation/4-prompts-para-candidatar-se-a-500-vagas-de-emprego.md) | Sistema de automação para candidaturas em massa

### 💼 Career - Carreira
- [7 Prompts para Recolocação Profissional](prompts/career/7-prompts-para-recolocacao-profissional.md) | Estratégias completas de reposicionamento de carreira

### 🚀 Entrepreneurship - Empreendedorismo
- [7 Prompts para Ganhar Dinheiro no YouTube](prompts/entrepreneurship/7-prompts-para-ganhar-dinheiro-no-youtube.md) | Estratégias de monetização e crescimento no YouTube
- [Análise de Chamada de Vendas](prompts/entrepreneurship/analise-de-chamada-de-vendas.md) | Analisa calls de vendas e extrai insights acionáveis
- [Comparação de Cotação de Fornecedores](prompts/entrepreneurship/comparacao-de-cotacao-de-fornecedores.md) | Avalia propostas de fornecedores de forma objetiva
- [Crie Conteúdo em Lote](prompts/entrepreneurship/crie-conteudo-em-lote.md) | Produção em massa de conteúdo com consistência de voz
- [Crie CTA que Gera Ação](prompts/entrepreneurship/crie-cta-que-gera-acao.md) | Calls-to-action de alta conversão
- [Crie Reels com Alta Retenção](prompts/entrepreneurship/crie-reels-com-alta-retencao.md) | Estrutura de roteiro para vídeos curtos que retêm audiência
- [Crie Stories que Prendem até o Final](prompts/entrepreneurship/crie-stories-que-prendem-ate-o-final.md) | Narrativa para Stories com alto índice de conclusão
- [Crie uma Oferta Irresistível](prompts/entrepreneurship/crie-uma-oferta-irresistivel.md) | Estrutura ofertas com alto poder de conversão
- [Descubra o que Faz seu Conteúdo Não Vender](prompts/entrepreneurship/descubra-o-que-faz-seu-conteudo-nao-vender.md) | Diagnóstico de conteúdo que não converte
- [E-mail de Recapitulação da Chamada de Vendas](prompts/entrepreneurship/e-mail-de-recapitulacao-da-chamada-de-vendas-vendas.md) | E-mail pós-call que reforça o valor e mantém o momentum
- [Escreva de Diferentes Perspectivas](prompts/entrepreneurship/escreva-de-diferentes-perspectivas.md) | Varia o ponto de vista para enriquecer o conteúdo
- [Escreva em Estilos ou Tons Diferentes](prompts/entrepreneurship/escreva-em-estilos-ou-tons-diferentes.md) | Adapta o tom para diferentes públicos e contextos
- [Estratégia de Engenharia Reversa do Algoritmo](prompts/entrepreneurship/estrategia-de-engenharia-reversa-do-algoritmo-e-alcance-massivo-com-perfil-zero.md) | Alcance massivo mesmo partindo do zero
- [Extrator de Inteligência Competitiva](prompts/entrepreneurship/extrator-de-inteligencia-competitiva-web-scraping-companion.md) | Mapeia concorrentes e extrai dados estratégicos
- [Gerador Criativo de Anúncios de IA (DALL·E ou Midjourney)](prompts/entrepreneurship/gerador-criativo-de-anuncios-de-ia-dalle-ou-midjourney.md) | Prompts visuais otimizados para anúncios com IA generativa
- [Gerador de Anúncios Visuais para Instagram e Facebook](prompts/entrepreneurship/gerador-de-anuncios-visuais-para-instagram-e-facebook-imagem-mais-ideia-de-texto.md) | Conceito visual + copy para anúncios nas redes sociais
- [Gerador de Cold E-mail Hiper-Personalizado](prompts/entrepreneurship/gerador-de-cold-e-mail-hiper-personalizado.md) | E-mails de prospecção com altíssima taxa de abertura
- [Gerador de Cópias de Marketing Orientado por Dados](prompts/entrepreneurship/gerador-de-copias-de-marketing-orientado-por-dados.md) | Copy baseado em dados de audiência e mercado
- [Gerador de Newsletter Semanal](prompts/entrepreneurship/gerador-de-newsletter-semanal-resumo-semanal.md) | Template completo para newsletters de valor
- [Gerador de Postagens de Mídia Social](prompts/entrepreneurship/gerador-de-postagens-de-midia-social-marketing.md) | Posts otimizados para diferentes plataformas
- [Gerador de Sequência de Cold E-mail em 3 Etapas](prompts/entrepreneurship/gerador-de-sequencia-de-cold-e-mail-em-3-etapas.md) | Sequência de follow-up que mantém o engajamento
- [Gerador de Variantes de Manchete (Pronto para Teste A/B)](prompts/entrepreneurship/gerador-de-variantes-de-manchete-pronto-para-teste-a-b.md) | Múltiplas versões de headline para testes A/B
- [Gere Ideias que Vendem](prompts/entrepreneurship/gere-ideias-que-vendem.md) | Brainstorm de ideias com potencial comercial real
- [Hook Criativo de Anúncio + Gerador de Pares Visuais](prompts/entrepreneurship/hook-criativo-de-anuncio-mais-gerador-de-pares-visuais.md) | Hooks persuasivos combinados com conceitos visuais
- [Identificando Oportunidades Comerciais usando o Google Maps](prompts/entrepreneurship/identificando-oportunidades-comerciais-usando-o-google-maps.md) | Prospecção de negócios locais via Google Maps
- [Lead Scoring Comportamental + Firmográfico](prompts/entrepreneurship/lead-scoring-comportamental-firmografico.md) | Qualificação automática de leads por comportamento
- [Lembrete de Pagamento de Fatura](prompts/entrepreneurship/lembrete-de-pagamento-de-fatura-financas.md) | E-mails de cobrança educados e eficazes
- [Obter Ideias de Conteúdo](prompts/entrepreneurship/obter-ideias-de-conteudo.md) | Geração de pautas alinhadas ao público-alvo
- [Resposta de Feedback do Cliente](prompts/entrepreneurship/resposta-de-feedback-do-cliente-suporte-marketing.md) | Respostas empáticas e profissionais a feedbacks
- [Roubando Reels Virais no Instagram](prompts/entrepreneurship/roubando-reels-virais-no-instagram.md) | Adapta conteúdo viral para sua marca com ética
- [Scanner de Risco de Contrato](prompts/entrepreneurship/scanner-de-risco-de-contrato.md) | Identifica cláusulas problemáticas em contratos
- [Simule sua Audiência](prompts/entrepreneurship/simule-sua-audiencia.md) | Simula reações do público-alvo ao seu conteúdo
- [Simule um Especialista](prompts/entrepreneurship/simule-um-especialista.md) | Configura a IA como especialista de domínio específico
- [Sugestão para Ideias de SEO](prompts/entrepreneurship/sugestao-para-ideias-de-seo.md) | Geração de pautas e palavras-chave com foco em SEO
- [Transforme Conhecimento em Produto](prompts/entrepreneurship/transforme-conhecimento-em-produto.md) | Estrutura seu expertise em produto digital vendável
- [Transforme Ideia Simples em Conteúdo Viral](prompts/entrepreneurship/transforme-ideia-simples-em-conteudo-viral.md) | Adapta qualquer ideia para formato viral

### 💰 Finance - Finanças
- [11 Prompts para Organizar as Finanças Pessoais](prompts/finance/11-prompts-para-organizar-as-financas-pessoais.md) | Série completa de organização financeira pessoal
- [Organização das Finanças](prompts/finance/organizacao-das-financas.md) | Estrutura orçamento e controle de gastos
- [Resumo Diário do Fluxo de Caixa](prompts/finance/resumo-diario-do-fluxo-de-caixa-financas.md) | Dashboard diário de entradas e saídas
- [Solicitação do Agente para Verificador de Relatório Financeiro](prompts/finance/solicitacao-do-agente-para-verificador-de-relatorio-financeiro.md) | Agente autônomo de verificação de relatórios financeiros

### 🎨 Image - Fotos e Imagens
- [3 Prompts para Criar Fotos de Perfil para Doutores](prompts/image/3-prompts-para-criar-fotos-de-perfil-para-doutores.md) | Fotos profissionais de perfil para área médica
- [3 Prompts para Criar Fotos Profissionais Realistas](prompts/image/3-prompts-para-criar-fotos-profissionais-realistas.md) | Fotos de alta qualidade com aparência fotográfica real
- [9 Prompts para Edição e Geração de Imagens com Nano Banana](prompts/image/9-prompts-para-edicao-e-geracao-de-imagens-com-nano-banana.md) | Coleção de prompts visuais avançados
- [Foto com Desenho a Caneta](prompts/image/foto-com-desenho-a-caneta.md) | Estilo artístico de esboço a caneta
- [Foto com Sombras Marcantes](prompts/image/foto-com-sombras-marcantes.md) | Fotografia com contraste e iluminação dramáticos
- [Melhoria em Fotos a partir de um JSON](prompts/image/melhoria-em-fotos-a-partir-de-um-json.md) | Melhora fotos com base em parâmetros estruturados

### 📚 Learn - Aprendizado
- [7 Prompts para Habilidades de Aprendizagem](prompts/learn/7-prompts-para-habilidades-de-aprendizagem.md) | Kit completo de técnicas de aprendizado
- [Aceleração de Aprendizado](prompts/learn/aceleracao-de-aprendizado.md) | Técnicas baseadas em ciência cognitiva para aprender mais rápido
- [Aprender algo do Zero](prompts/learn/aprender-algo-do-zero.md) | Roadmap completo para iniciar em qualquer área
- [Dominar Qualquer Habilidade GRÁTIS](prompts/learn/dominar-qualquer-habilidade-gratis.md) | Sequência de estudo sem custos para dominar skills
- [Entender Algo como um Gênio](prompts/learn/entender-algo-como-um-genio.md) | Compreensão profunda usando método Feynman
- [Estudar para Provas](prompts/learn/estudar-para-provas.md) | Estratégias de revisão e memorização para avaliações
- [Explicar um Tema](prompts/learn/explicar-um-tema.md) | Explica qualquer assunto com clareza progressiva
- [Obtenha um Nível de Doutorado](prompts/learn/obtenha-um-nivel-de-doutorado.md) | Mergulho acadêmico profundo em qualquer tema
- [Transforme Confusão em Clareza](prompts/learn/transforme-confusao-em-clareza.md) | Resolve mal-entendidos e simplifica conceitos complexos
- [Use Diferentes Formatos para Obter Conhecimento](prompts/learn/use-diferentes-formatos-para-obter-conhecimento-sobre-um-assunto.md) | Varia o formato de estudo para maximizar retenção

### 🏢 Management - Gestão
- [7 Prompts Estratégicos para Gestão de Pessoas e Tempo](prompts/management/7-prompts-estrategicos-para-gestao-de-pessoas-e-tempo.md)           | Framework de liderança e produtividade
- [Acompanhamento de Candidato a Emprego (RH)](prompts/management/acompanhamento-de-candidato-a-emprego-rh.md)                                   | Pipeline de comunicação com candidatos em processo seletivo
- [Agente de Agendamento Automático](prompts/management/agente-de-agendamento-automatico-calendario-e-integracao-de-e-mail.md)                   | Automação de calendário e e-mails
- [Anúncio Interno de Novo Contratado](prompts/management/anuncio-interno-de-novo-contratado-rh-admin.md)                                        | Comunicado de boas-vindas para novos colaboradores
- [Classificador de E-mail de Suporte ao Cliente](prompts/management/classificador-de-e-mail-de-suporte-ao-cliente-deteccao-de-intencao.md)      | Categoriza automaticamente e-mails de suporte por intenção
- [Conversor de POP para Guia de Integração](prompts/management/conversor-interno-de-procedimento-operacional-padrao-para-guia-de-integracao.md) | Transforma POPs em guias de onboarding acessíveis
- [Organização de Tarefas para o Dia a Dia](prompts/management/organizacao-de-tarefas-para-o-dia-a-dia.md)                                       | Priorização inteligente da agenda diária
- [Planejamento Estratégico](prompts/management/planejamento-estrategico.md)                                                                     | Estrutura planos estratégicos de curto e longo prazo
- [Planejamento Semanal](prompts/management/planejamento-semanal.md)                                                                             | Revisão e planejamento estruturado da semana
- [Priorização de Tarefas Diárias](prompts/management/priorizacao-de-tarefas-diarias-admin-operacoes.md)                                         | Ordena tarefas por urgência e impacto
- [Resumo da Reunião com Itens de Ação](prompts/management/resumo-da-reuniao-com-itens-de-acao-admin.md)                                         | Ata automática com action items claros
- [Resumo Executivo de Dados Brutos](prompts/management/resumo-executivo-de-dados-brutos.md)                                                     | Transforma dados brutos em insights executivos
- [Reunião → Resumo de Acompanhamento + Gerador de Tarefas](prompts/management/reuniao-resumo-de-acompanhamento-gerador-de-tarefas.md)           | Pipeline completo de pós-reunião com tarefas geradas

### 🧘 Personal - Vida Pessoal
- [3 Prompts para Mapear Árvore Genealógica](prompts/personal/3-prompts-para-mapear-arvore-genealogica.md) | Pesquisa e visualização de genealogia familiar
- [7 Prompts Inteligentes para Compras Online](prompts/personal/7-prompts-inteligentes-para-compras-online.md) | Decisões de compra mais inteligentes com IA
- [Decisões Cotidianas](prompts/personal/decisoes-cotidianas.md) | Suporte para decisões do dia a dia com clareza
- [Melhore Seu Cérebro em 30 Dias](prompts/personal/melhore-seu-cerebro-em-30-dias.md) | Plano de desenvolvimento cognitivo mensal
- [Planejamento Pessoal](prompts/personal/planejamento-pessoal.md) | Organização da vida pessoal com foco e clareza

### ✍️ Text - Escrita e Comunicação
- [4 Prompts para Escrita e Comunicação](prompts/text/4-prompts-para-escrita-e-comunicacao.md) | Técnicas essenciais de comunicação escrita
- [6 Prompts para Eliminar a Estrutura Artificial dos Textos Gerados](prompts/text/6-prompts-para-eliminar-a-estrutura-artificial-dos-textos-gerados.md) | Remove padrões óbvios de texto gerado por IA
- [Aplique Técnicas de Escrita Humana](prompts/text/aplique-tecnicas-de-escrita-humana.md) | Humanize textos gerados por IA
- [Avaliação Crítica de Textos](prompts/text/avaliacao-critica-de-textos.md) | Análise profunda de qualidade textual
- [Capture seu Estilo de Escrita](prompts/text/capture-seu-estilo-de-escrita.md) | Replica seu estilo pessoal de escrita fielmente
- [Criar Estrutura de Texto sobre um Tema](prompts/text/criar-estrutura-de-texto-sobre-um-tema.md) | Esqueleto narrativo para qualquer tipo de texto
- [Questione a Narrativa Convencional](prompts/text/questione-a-narrativa-convencional.md) | Perspectivas alternativas e contra-intuitivas
- [Reescrever para Obter Maior Clareza](prompts/text/reescrever-para-obter-maior-clareza.md) | Simplifica textos complexos sem perder profundidade
- [Respondente de E-mail de Tratamento de Objeções](prompts/text/respondente-de-e-mail-de-tratamento-de-objecoes-vendas.md) | Respostas a objeções que mantêm a negociação viva
- [Resumo de Conteúdos](prompts/text/resumo-de-conteudos.md) | Condensa textos longos preservando o essencial

## 🧠 Skills
Skills são instruções estruturadas que transformam uma IA em um especialista com comportamento consistente e repetível. Funcionam com **Claude Code**, **Github Copilot**, **Antigravity** e qualquer agente que suporte arquivos de contexto.

> [!NOTE]
> **Como usar**
> Copie o arquivo `.md` para a pasta de skills do seu agente (ex.: `~/.claude/skills/`) ou referencie no contexto do sistema.

- [Arte Publicitária para Vendas](skills/arte-publicitaria-para-vendas.md) | Cria conceitos visuais e cópias para anúncios de alta conversão
- [Aumentar Qualidade das Imagens](skills/aumentar-qualidade-das-imagens.md) | Melhora prompts de imagem para resultados mais detalhados e realistas
- [Coach de Escrita](skills/coach-de-escrita.md) | Revisão e aprimoramento de textos com tom humano e natural
- [Coach de Tradução](skills/coach-de-traducao.md) | Traduções contextuais que preservam nuance e intenção
- [Criador de Projeto .NET do Zero](skills/criador-de-projeto-dotnet-do-zero.md) | Scaffolding completo de projetos .NET com boas práticas
- [Gerador de Documentações para Projetos no Github](skills/gerador-de-documentacao-padrao-github.md) | Gera README e afins no padrão Github a partir de um código ou descrição
- [Redigir Currículo](skills/redigir-curriculo.md) | Cria e otimiza currículos para ATS e recrutadores humanos

## 🤝 Contribuindo
Este repositório não faz parte da lista [![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re), mas qualquer boa contribuição é bem-vinda: prompts, skills, artigos, dicas, correções e melhorias.

Leia o **[Guia de Contribuição](CONTRIBUTING.md)** completo antes de abrir um PR. Ele cobre:
- Tipos de contribuição aceitos
- Padrão obrigatório de nomenclatura (`kebab-case`)
- Frontmatter de skills e convenção de variáveis `{{VARIAVEIS}}`
- Passo a passo para cada tipo de conteúdo
- Checklist e formato de Pull Request

> [!TIP]
> **Não sabe onde colocar?**
> Abra uma [Issue](../../issues) com o título **[Categoria]** e vamos ajudar a categorizar.

## 📄 Licença
[MIT License](LICENSE). Sinta-se livre para usar, adaptar e compartilhar.

---
Feito com ☕ e muitos prompts testados na prática.

**Se este repositório te ajudou, deixe uma ⭐**
