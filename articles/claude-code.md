---
title: "Claude Code"
category: "articles"
target_model: "Claude"
---

# Claude Code
## Introdução
O Claude Code não é apenas um "chat", mas um **agente de terminal** que interage diretamente com o teu sistema. Para ele ser eficaz, o programador deixa de ser um "digitador" e passa a ser um **arquiteto** e **revisor**. Não é uma "varinha mágica" que substitui o programador, mas sim um **agente colaborador** extremamente potente. A ideia central é que a IA performa melhor quando o código humano é organizado, bem testado e documentado. O autor defende que, se souberes orquestrar a ferramenta, podes deixar de "escrever código à mão" para te focares em **projetar** e **validar** soluções.

Pensa no Claude Code como um estagiário genial, mas que precisa de ordens claras. Se o teu escritório (o código) estiver uma bagunça, ele vai tropeçar nos papéis. Se estiver organizado, ele trabalha à velocidade da luz!

Para dominarmos este tema, preparei um plano de aprendizagem com 3 passos simples:
1. **O Fluxo de Trabalho Ideal**: Por que o modo "Plan" é o teu melhor amigo.
2. **Documentação Inteligente**: O poder do arquivo CLAUDE.md e a "divulgação progressiva".
3. **Qualidade e Simbiose**: Como testes e código limpo ajudam a IA a ajudar-te.

### Antes de qualquer coisa, a dica metacognitiva
Ao ler sobre ferramentas de IA, tenta não focar apenas no "o que ela faz", mas no "como eu mudo o meu processo para tirar proveito dela". É a diferença entre usar um trator como se fosse uma enxada ou usá-lo para arar um campo inteiro!

### O Fluxo: Planeamento antes da Ação
Nunca peças à IA para escrever código logo no primeiro comando. O autor sugere o **modo "plan"**:
- **Como funciona**: O Claude lê a base de código (sem alterar nada) e propõe um plano de ação.
- **O teu papel**: Validar se o plano cobre casos de erro (edge cases), testes e documentação. Só autorizas a escrita quando o plano estiver sólido.

### O Segredo: Arquivos CLAUDE.md
A IA tem limites de "memória" (contexto). Para ela não se perder ou gastar recursos desnecessários:
- **Divulgação Progressiva**: Não coloques tudo num único arquivo gigante. Cria um CLAUDE.md na raiz com o essencial (como rodar o projeto, estilo de código) e usa subarquivos para detalhes específicos.
- **Automação**: O comando /init cria a base, mas a manutenção manual (ou via skills) garante que a IA saiba exatamente onde está cada peça do puzzle.    

### Simbiose: Qualidade de Código = Performance da IA
Existe um mito de que, se a IA escreve, o código pode ser "sujo". O artigo prova o contrário:
- **Testes são Vitais**: O Claude Code consegue rodar testes sozinho. Se houver erro, ele tenta corrigir-se. Sem testes, ele não tem como saber se estragou algo.
- **Clean Code**: Padrões como DRY (não repetir código) e nomes claros de variáveis ajudam a IA a gastar menos "tokens" e a entender a lógica mais rápido.

## Criando o primeiro CLAUDE.md
Ao escreveres o teu CLAUDE.md, estás a fazer um exercício de Autoexplicação. Isso ajuda-te a organizar o teu próprio pensamento sobre a arquitetura do teu sistema. Se não conseguires explicar à IA como o código deve ser escrito, talvez a arquitetura ainda não esteja clara para ti!

### O Atalho Inicial
O Claude Code tem um comando nativo para isto. No teu terminal, dentro da pasta do projeto, digita: `/init`.

Isso vai gerar um rascunho básico com base no que a IA conseguir ler nos teus ficheiros (linguagem, framework, etc.). **Mas atenção**: o arquivo automático costuma ser apenas "ok". É necessário refinar!

### A Estrutura Ideal (O que deve conter)
Um bom CLAUDE.md deve ser direto. Aqui tens as seções essenciais que deves incluir ou editar:
- **Comandos de Build e Teste**: Como é que ele compila o código? Como é que ele corre os testes? (ex: npm test, pytest, dotnet build).
- **Estilo de Código (Coding Style)**: Tu preferes indentação com 2 espaços ou 4? Usas PascalCase ou camelCase?
- **Decisões Arquiteturais**: Onde ficam as rotas? Onde estão os modelos de base de dados    
- **Erros Comuns / "Gotchas"**: Existe alguma biblioteca que costuma dar erro se não for usada de certa forma?

### Exemplo Prático de Conteúdo
Podes copiar e adaptar este modelo para o teu ficheiro:

```markdown
# Orientações do Projeto XYZ

## Comandos Úteis
- Build: `npm run build`
- Testes: `npm test`
- Lint: `npm run lint`

## Padrões de Código
- Usar TypeScript com tipagem estrita.
- Funções devem ser curtas e seguir o princípio de responsabilidade única.
- Preferir `async/await` em vez de `.then()`.

## Estrutura de Pastas
- `/src/components`: Componentes visuais.
- `/src/services`: Chamadas à API.
```

### A Estratégia da "Divulgação Progressiva"
Lembra-te do que o artigo mencionou: **não deixes o arquivo ficar gigante**. Se o teu projeto crescer muito (ex: um sistema com Front-end e Back-end na mesma pasta), faz o seguinte:
1. No CLAUDE.md da raiz, coloca apenas o geral.
2. Cria um CLAUDE.md dentro da pasta /backend com as regras específicas de lá.
3. A IA só vai ler o manual específico quando estiver a trabalhar naquela pasta!

## A Nova Era: "Não escrever código à mão"
A conclusão é audaciosa: o desenvolvimento "tradicional" está a mudar.
- A IA preenche lacunas de memória do programador (detalhes de APIs, libs).    
- O foco do humano desloca-se para a **estratégia** e **resolução de problemas complexos**, enquanto a IA executa a implementação técnica seguindo as regras definidas.

Ref.: [https://code.claude.com/docs/pt/overview](https://code.claude.com/docs/pt/overview)

## Configuração para um projeto de assistente pessoal
### Camada de memória
Em vez de um único grande CLAUDE.md, eu dividi em `.claude/rules/memory-*.md` arquivos — perfil (fatos sobre mim), preferências (como gosto que as coisas sejam feitas), decisões (escolhas passadas para consistência) e sessões (resumo contínuo do trabalho recente). O Claude Code carrega automaticamente tudo em `.claude/rules/`, então está sempre em contexto sem encher o main CLAUDE.md.

### Execução
O CLAUDE.md tem uma seção OBRIGATÓRIA dizendo ao Claude para atualizar os arquivos de memória à medida que avança, não no final. O problema é que o Claude "esquece" instruções no meio da sessão, então eu adicionei um _hook_ de Parada que verifica se arquivos propensos a aprendizado mudaram e lembra de capturar qualquer coisa nova. Cinto e _suspenders_.

### MCP
O maior desbloqueio para mim foi conectar ferramentas que o Claude não consegue acessar nativamente. Automação do navegador para pesquisa, Google Workspace para e-mail/calendário, Reddit para monitoramento — transforma o Claude Code de uma ferramenta de codificação em um assistente de verdade.

### A maioria das pessoas não percebe que...
O CLAUDE.md deve ser um arquivo de roteamento, não um depósito de conhecimento. Mantenha com menos de 150 linhas. Aponte para `.claude/rules/*.md` para especificações detalhadas e `docs/` para arquitetura. Caso contrário, fica tão longo que o Claude lê por cima e perde as informações importantes.

### Atualizar os arquivos de memória
#### Instrução CLAUDE.md
Carregada automaticamente a cada sessão:

```markdown
### Auto-Update Memory (MANDATORY)
**Update memory files AS YOU GO, not at the end.** When you learn something new, update immediately.

| Trigger                             | Action                                    |
|-------------------------------------|-------------------------------------------|
| User shares a fact about themselves | → Update `memory-profile.md`              |
| User states a preference            | → Update `memory-preferences.md`          |
| A decision is made                  | → Update `memory-decisions.md` with date  |
| Completing substantive work         | → Add to `memory-sessions.md`             |

**Skip:** Quick factual questions, trivial tasks with no new info.

**DO NOT ASK. Just update the files when you learn something.**
```

As linhas chave são "À MEDIDA QUE FOR, não no final" e "NÃO PERGUNTE." Sem ambas, tende a esquecer ou pedir permissão toda vez.

#### Hook de parada
settings.json → hooks.Stop:

```bash
#!/bin/bash
CONTEXT=$(cat)

STRONG_PATTERNS="fixed|workaround|gotcha|that's wrong|check again|we already|should have|discovered|realized|turns out"
WEAK_PATTERNS="error|bug|issue|problem|fail"

if echo "$CONTEXT" | grep -qiE "$STRONG_PATTERNS"; then
    cat << 'EOF'
{
  "decision": "approve",
  "systemMessage": "This session involved fixes or discoveries. Consider running /reflect to capture learnings in project docs."
}
EOF
elif echo "$CONTEXT" | grep -qiE "$WEAK_PATTERNS"; then
    echo '{"decision":"approve","systemMessage":"If you learned something non-obvious this session, run /reflect to update docs."}'
else
    echo '{"decision": "approve"}'
fi
```

Isso é executado quando uma sessão termina. Ele faz o reconhecimento de padrões da conversa em busca de sinais de que o aprendizado aconteceu (correções, descobertas, soluções alternativas) e incentiva Claude a anotá-los. É uma rede de segurança — a instrução CLAUDE.md lida com ~90% disso, mas o gancho captura as sessões em que ele esqueceu.

Os arquivos de memória em si vivem em `.claude/rules/`, então são carregados automaticamente como contexto a cada sessão. Sem RAG, sem _embeddings_ — apenas arquivos markdown simples que Claude lê na inicialização e edita no local.

## Referências
- https://claude.com/product/claude-code
- https://www.linkedin.com/pulse/claude-code-e-o-fim-do-desenvolvimento-como-conhecemos-marco-souza-0gpzf/
- https://github.com/oprogramadorreal/claude-code-bootstrap