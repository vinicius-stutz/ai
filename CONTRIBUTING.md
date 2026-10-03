# 🤝 Guia de Contribuição

Obrigado por querer contribuir com este repositório! Toda contribuição — seja um novo prompt, uma skill aprimorada, uma correção ou uma dica — ajuda a comunidade a usar IA com mais eficiência e intenção.

Leia este guia antes de abrir um Pull Request.

## 📋 Índice

- [Tipos de contribuição](#tipos-de-contribuição)
- [Antes de começar](#antes-de-começar)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Padrões obrigatórios](#padrões-obrigatórios)
  - [Nomenclatura de arquivos](#nomenclatura-de-arquivos)
  - [Frontmatter de skills](#frontmatter-de-skills)
  - [Variáveis de prompt](#variáveis-de-prompt)
- [Como adicionar um prompt](#como-adicionar-um-prompt)
- [Como adicionar uma skill](#como-adicionar-uma-skill)
- [Como adicionar um artigo ou dica](#como-adicionar-um-artigo-ou-dica)
- [Abrindo um Pull Request](#abrindo-um-pull-request)
- [Reportando problemas](#reportando-problemas)
- [Código de conduta](#código-de-conduta)

---

## Tipos de contribuição

| Tipo | O que é | Onde vai |
|------|---------|----------|
| **Prompt** | Instrução para uma IA realizar uma tarefa específica | `prompts/<categoria>/` |
| **Skill** | Arquivo de contexto que define um agente especialista | `skills/` |
| **Artigo** | Guia ou explicação aprofundada sobre IA | `articles/` |
| **Dica** | Técnica rápida ou truque prático | `tips/` |
| **Configuração** | Instrução de sistema para personalizar uma IA | `config/` |
| **Comando** | Atalho ou comando rápido para LLMs | `commands/` |
| **Correção** | Typo, link quebrado, formatação incorreta | Qualquer arquivo |

## Antes de começar
1. **Verifique se já existe** algo semelhante no repositório. Busque pelo tema antes de criar um arquivo novo.
2. **Teste seu prompt** — contribua apenas com conteúdo que você já usou e validou.
3. **Prefira qualidade a quantidade** — um prompt bem descrito vale mais do que dez genéricos.
4. **Não inclua dados pessoais** — substitua por variáveis (`{{SEU_NOME}}`).

## Estrutura do repositório
```
.
├── articles/             # Guias aprofundados sobre IA e agentes
├── commands/             # Comandos rápidos para LLMs no dia a dia
├── config/               # Configurações de comportamento para IAs
├── prompts/
│   ├── analysis/         # Análise, pesquisa e tomada de decisão
│   ├── automation/       # Automação de tarefas e rotinas
│   ├── career/           # Carreira e recolocação profissional
│   ├── entrepreneurship/ # Empreendedorismo, marketing e vendas
│   ├── finance/          # Finanças pessoais e corporativas
│   ├── image/            # Geração e edição de imagens
│   ├── learn/            # Aprendizado acelerado e estudos
│   ├── management/       # Gestão de pessoas, tempo e reuniões
│   ├── personal/         # Vida pessoal e produtividade
│   └── text/             # Escrita, comunicação e copywriting
├── skills/               # Skills para Claude Code e agentes de IA
└── tips/                 # Dicas práticas de ferramentas e IA
```

> [!TIP]
> 
> **Não sabe em qual pasta colocar?**
> 
> Abra uma [Issue](../../issues) com o título **[Categoria]** e descreva o conteúdo — vamos ajudar.

## Padrões obrigatórios
### Nomenclatura de arquivos
Todos os arquivos **devem usar `kebab-case`**: letras minúsculas, palavras separadas por hífens, sem espaços, acentos ou caracteres especiais.

| ❌ Errado | ✅ Correto |
|-----------|-----------|
| `Meu Prompt.md` | `meu-prompt.md` |
| `Análise de Dados.md` | `analise-de-dados.md` |
| `prompt_vendas.md` | `prompt-vendas.md` |
| `ColdEmail(Vendas).md` | `cold-email-vendas.md` |

**Tabela de substituição de caracteres especiais:**

| Caractere | Substituto |
|-----------|-----------|
| `á â à ã` | `a` |
| `é ê` | `e` |
| `í` | `i` |
| `ó ô õ` | `o` |
| `ú ü` | `u` |
| `ç` | `c` |
| `ñ` | `n` |
| `( )` | removido |
| `+` | `-mais-` |
| `→` | `-para-` |
| `&` | `-e-` |
| espaço / `_` | `-` |

### Frontmatter de skills
Todo arquivo na pasta `skills/` **deve começar** com o bloco de frontmatter YAML:

```yaml
---
name: "Título legível da skill"
description: "Uma frase descrevendo o que a skill faz e para quem é útil."
---
```

**Exemplo completo:**
```yaml
---
name: "Coach de Escrita"
description: "Revisa e aprimora textos, ajustando tom, clareza e naturalidade sem alterar a voz do autor."
---

## Contexto
Você é um coach de escrita especializado em comunicação clara e persuasiva...
```

### Variáveis de prompt
Use **duplas chaves** para marcar qualquer dado que o usuário deverá substituir pelo seu próprio contexto:

```
{{NOME_DA_VARIAVEL}}
```

**Convenções:**

- Sempre em **MAIÚSCULAS**
- Use **underscores** para separar palavras: `{{MEU_PRODUTO}}`, `{{PUBLICO_ALVO}}`
- Seja descritivo: prefira `{{NOME_DA_EMPRESA}}` a `{{EMPRESA}}`
- Documente as variáveis no início do prompt com uma lista explicativa

**Exemplo:**

```markdown
## Variáveis
- `{{PRODUTO}}` — Nome do produto ou serviço sendo promovido
- `{{PUBLICO_ALVO}}` — Descrição do perfil do cliente ideal
- `{{TOM}}` — Tom desejado: formal, descontraído, técnico, inspirador

Você é um especialista em copywriting. Crie 5 variações de headline para {{PRODUTO}},
direcionadas a {{PUBLICO_ALVO}}, usando o tom {{TOM}}...
```

## Como adicionar um prompt
1. **Identifique a categoria** correta em `prompts/`
2. **Crie o arquivo** com nome em `kebab-case`
3. **Estruture o conteúdo** seguindo o template:

```markdown
# Título do Prompt

Descrição curta do objetivo do prompt.

## Variáveis
- `{{VARIAVEL_1}}` — O que ela representa
- `{{VARIAVEL_2}}` — O que ela representa

## Prompt
[Corpo do prompt aqui, com as variáveis marcadas com duplas chaves]
```

4. **Adicione a entrada no README.md** na tabela da categoria correspondente
5. **Abra o Pull Request**

## Como adicionar uma skill

1. **Crie o arquivo** em `skills/` com nome em `kebab-case`
2. **Inclua o frontmatter** YAML obrigatório no início
3. **Escreva as instruções** de forma clara, como se fosse um system prompt completo
4. **Estrutura recomendada:**

```markdown
---
name: "Nome da Skill"
description: "O que a skill faz em uma frase."
---

## Contexto

[Quem é o agente, qual sua especialidade e propósito]

## Comportamento

[Como o agente deve se comportar, responder e se comunicar]

## Capacidades

[Lista de o que o agente pode fazer]

## Limitações

[O que o agente deve evitar ou recusar]

## Formato de resposta

[Como as respostas devem ser estruturadas]
```

5. **Adicione a entrada no README.md** na tabela de Skills
6. **Abra o Pull Request**

## Como adicionar um artigo ou dica

- **Artigos** (`articles/`): guias mais longos, com exemplos, contexto e raciocínio. Mínimo sugerido de 500 palavras.
- **Dicas** (`tips/`): conteúdo direto ao ponto — uma técnica, um truque, um passo a passo curto.

Ambos devem ter um **título claro** como primeira linha (`# Título`) e usar markdown padrão.

## Abrindo um Pull Request
### Checklist antes de submeter
- [ ] Nome do arquivo em `kebab-case` sem acentos ou caracteres especiais
- [ ] Skills têm frontmatter YAML completo (`name` e `description`)
- [ ] Prompts usam `{{VARIAVEIS}}` para dados contextuais
- [ ] README.md atualizado com o link para o novo arquivo (se aplicável)
- [ ] Conteúdo testado e validado na prática
- [ ] Nenhum dado pessoal no conteúdo

### Título do PR
Use o formato: `[tipo] Descrição breve`

Exemplos:
- `[prompt] Gerador de bio profissional para LinkedIn`
- `[skill] Analista de contratos jurídicos`
- `[fix] Corrige link quebrado em skills/coach-de-escrita.md`
- `[article] Como usar agentes com múltiplos arquivos de contexto`

### Corpo do PR
Descreva brevemente:
- **O que** foi adicionado ou corrigido
- **Por que** é útil
- **Como** foi testado (qual IA, qual contexto)

## Reportando problemas
Encontrou um prompt que não funciona bem, um link quebrado ou algo desatualizado?

[Abra uma Issue](../../issues) com:
- Título descritivo
- O arquivo afetado
- O que acontece vs. o que deveria acontecer
- (Opcional) Sugestão de correção

---
[Código de conduta](./CODE_OF_CONDUCT.md)

Feito com ☕ Obrigado por fazer parte disso 🙏
