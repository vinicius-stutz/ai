---
name: gerador-de-documentacao-readme
description: Gerador de README.md e arquivos de documentação padrão para projetos de desenvolvimento, com foco em .NET, C#, JavaScript e ReactJS.
---
# Gerador de Documentação README
Ao pedir para documentar algo em arquivo markdown (especialmente o README.md), analise o projeto aberto e gere a documentação seguindo os padrões de mercado difundidos para construção de arquivos LEIA-ME (README.md) de projetos de desenvolvimento em repositórios públicos do GitHub.

Pensando nos padrões adotados pelo Github, esta skill cria ou atualiza os seguintes arquivos na raiz do repositório:
- `README.md`
- `CODE_OF_CONDUCT.md`
- `CONTRIBUTING.md`
- `LICENSE` (sem extensão)
- `SECURITY.md`

---
## O arquivo README.md
### Primeira linha do arquivo README.md
Um bloco de código contendo uma ASCII Art, dentro do contexto do projeto, criativa (divertida, se possível), que funcione como uma *hero image* para o README.

### 1. PROJECT TITLE
Esta seção deve ter seu conteúdo todo centralizado. A primeira linha deve ter uma seção com o Título do Projeto (usando a tag `<h1>`), com o seu conteúdo todo centralizado, contendo informações rápidas resumidas.

A segunda linha deve conter apenas as PROJECT SHIELDS (em ordem, todos na mesma linha separados apenas por um espaço):
- `version` (versão do projeto principal)
- `language` (da stack principal, com a versão)
- `status build` do projeto - normalmente o usuário informará o serviço com o link da badge, caso contrário, ele informará o status:
  - **Não monitorado:** dimgray + gray
  - **Sucesso:** dimgray + green
  - **Falha:** dimgray + red
- `license` (licença do projeto)
- botão *follow* do Github para o owner do repositório, algo como o exemplo `<a href="https://github.com/username" target="_blank"><img src="https://img.shields.io/github/followers/username?label=follow&style=social" height="20" title="Siga-me!" alt="Siga-me!" /></a>`

A última linha desta seção deve conter links como:
- Link para a documentação do projeto (ex: uma Wiki dentro do próprio Github Repo etc)
- Link para Issues (ex: dentro do próprio Github Repo)
- Link para Pull Requests (ex: dentro do próprio Github Repo)
- Links para as Release Notes (se existirem)
 
Exemplo de como devem ficar as primeiras linhas do documento:
```html
<h1 align="center">Título do projeto aqui</h1>
<p align="center">
  PROJECT SHIELDS aqui
</p>

<p align="center">
  Links aqui
</p>
```

> A partir daqui o conteúdo não deve mais ser centralizado.
### 2. TABLE OF CONTENTS
A seguir, crie uma seção "Índice" (sem título), respeitando o uso de tags HTML:
```html
<details>
  <summary><b>Índice</b></summary>
  <ol>
  <li><a href="#sobre-o-projeto">Sobre o Projeto</a></li>
  <li><a href="#tecnologias">Tecnologias</a></li>
  <li><a href="#começando">Começando</a></li>
  <li><a href="#exemplos-de-uso">Exemplos de Uso</a></li>
  <li><a href="#roadmap">Roadmap</a></li>
  <li><a href="#contribuindo">Contribuindo</a></li>
  <li><a href="#licença">Licença</a></li>
  <li><a href="#contato">Contato</a></li>
  </ol>
</details>
```

> Tome a liberdade de alterar o índice conforme necessidade, adicionando ou removendo itens, mas sempre respeitando a hierarquia de tags HTML.

### 3. ABOUT THE PROJECT
Crie uma seção chamada "Sobre o Projeto", contendo:
- Breve descrição
- Propósito do projeto
- Contexto de negócio (os problemas que a aplicação resolve)
- Termos do domínio e seus significados
- Principais funcionalidades

### 4. BUILT WITH
Crie uma seção chamada "Tecnologias", contendo:
- Estilo arquitetural (Clean Architecture, Layered, Hexagonal, etc.), com um diagrama de camadas (usando Mermaid)
- Design patterns identificados (Repository, Factory, Strategy, etc.)
- Princípios SOLID aplicados (se aplicável para o tipo do projeto)
- Práticas de Clean Code (se aplicável para o tipo do projeto)
- Os principais frameworks, linguagens e ferramentas utilizadas no projeto, com links para suas documentações oficiais

#### Resiliência
Fale resumidamente sobre as práticas de resiliência aplicadas no projeto (se aplicável para o tipo do projeto):
- Retry policies
- Circuit breakers
- Fallback strategies
- Timeout configurations

#### Observabilidade
Fale resumidamente sobre as práticas de observabilidade aplicadas no projeto (se aplicável para o tipo do projeto):
- Logs (estrutura e níveis)
- Métricas coletadas
- Traces distribuídos
- Health checks

#### Escalabilidade
Fale resumidamente sobre as práticas de escalabilidade aplicadas no projeto (se aplicável para o tipo do projeto):
- Estratégias de scaling (horizontal/vertical)
- Stateless/stateful
- Limitações conhecidas

### 5. GETTING STARTED
Crie uma seção chamada "Começando", contendo:
- Pré-requisitos
- Instalação
- Estrutura do Projeto

### 6. USAGE EXAMPLES
Crie uma seção chamada "Exemplos de uso", contendo:
- Uso Básico do Serviço
- Configuração
- Trabalhando com Entidades (se aplicável para o tipo do projeto)
- Diagrama de classes do domínio (usando Mermaid, se aplicável para o tipo do projeto)

### 7. ROADMAP
Crie uma seção chamada "Roadmap". Caso o projeto esteja em processo de substituição ou descontinuação, informe explicitamente. Caso contrário, descreva as próximas evoluções planejadas para o projeto, realizando uma análise crítica. As áreas de análise devem ser as seguintes:
- **Boas Práticas**: Convenções de nomenclatura, uso de features modernas
- **Programação Assíncrona**: Uso correto de async/await, prevenção de deadlocks, CancellationToken
- **Domain-Driven Design**: Coesão dos agregados, separação de responsabilidades
- **Design Patterns**: Aplicação e oportunidades
- **SOLID**: Violações e correções
- **Segurança**: Vulnerabilidades, validação de inputs, exposição de dados sensíveis
- **Performance**: N+1 queries, alocação de memória, operações síncronas bloqueantes
- **Resiliência**: Pontos de falha e tratamento
- **Observabilidade**: Gaps na instrumentação
- **Testabilidade**: Dificuldades para testes unitários
- **Code Smells**: Duplicação, métodos longos, classes "God Object", acoplamento excessivo

Para cada sugestão, inclua:
- **Severidade**: Crítica, Alta, Média, Baixa
- **Categoria**: Performance, Segurança, Manutenibilidade, etc
- **Localização**: Arquivo e linha (quando aplicável)
- **Problema Atual**: Breve descrição do problema
- **Solução Proposta**: Como resolver
- **Benefícios**: Ganhos esperados

> **Importante**: Adote sempre uma visão de tabela para melhor apresentação das informações!

### 8. CONTRIBUTING
Crie uma seção chamada "Contribuindo". Deve ter um link para o arquivo CONTRIBUTING.md.

### 9. LICENSE
Crie uma seção "Licença" com o tipo de licença do projeto e um link para o arquivo LICENSE.

### 10. CONTACT
Crie uma seção "Contato" contendo:
- O nome da equipe (ou da pessoa) responsável (se não souber, pergunte ao usuário no prompt)
- Link para o perfil do colaborador no Github (se não souber, pergunte ao usuário no prompt)
- Links relevantes de documentação e gestão do projeto

### Últimas linhas do arquivo README.md
As últimas linhas devem conter:
- Uma linha separadora
- Um link para o arquivo CODE_OF_CONDUCT.md
- Um link para o arquivo SECURITY.md

---

## O arquivo CODE_OF_CONDUCT.md
```markdown
# Código de conduta para colaboradores
## Objetivo
Este repositório é mantido por {X} colaboradore(s). Espera-se que todas as contribuições priorizem qualidade, segurança, respeito e colaboração.

## Princípios
- Respeitar colegas e usuários.
- Manter discussões técnicas objetivas e profissionais.
- Buscar compartilhamento de conhecimento e colaboração.
- Registrar decisões relevantes de forma transparente.

## Desenvolvimento
Ao contribuir para este projeto:
- Siga os padrões de codificação predefinidos.
- Mantenha código simples, legível e testável.
- Evite duplicação desnecessária.
- Documente alterações relevantes.
- Considere impactos em segurança, desempenho e observabilidade.

## Pull Requests
- Todo código deve passar por revisão.
- Feedbacks devem ser construtivos e focados na solução.
- Divergências técnicas devem ser discutidas com base em fatos, evidências e requisitos de negócio.
- **Não aprove** alterações que **você não compreendeu** completamente.

## Segurança e Dados
- Nunca exponha credenciais, senhas, tokens ou chaves.
- Nunca utilize dados reais de pessoas e empresas em testes ou exemplos.
- Respeite políticas de segurança e legislações aplicáveis (LGPD, GDPR etc).
- Reporte imediatamente vulnerabilidades ou exposições identificadas.

## Responsabilidade Compartilhada
A qualidade, estabilidade e segurança do sistema são responsabilidades coletivas de quem colabora com o projeto. Ao identificar um problema, colabore para sua correção ou encaminhamento adequado.
```

Onde `{X}` é a quantidade de colaboradores.

---

## O arquivo CONTRIBUTING.md
Este projeto é versionado com git e adota o uso do GitFlow como padrão de branching.

### Testes unitários
Se fizer sentido para o tipo de projeto, inclua uma badge de cobertura de testes (gerada via relatório de cobertura) e documente:
- **Cobertura de Testes**: Percentual e áreas cobertas
- **Tipos de Testes**: Unitários, integração, end-to-end
- **Casos de Teste Críticos**: Cenários mais importantes
- **Mocks e Fixtures**: Estratégias de dublês de teste
- **Como Executar**: Comandos para rodar os testes
- **Gaps de Cobertura**: Áreas não testadas e recomendações

---

## O arquivo LICENSE
Substitua pelo conteúdo de licença adequado ao projeto (MIT, Apache 2.0, GPL, Proprietária etc).

---

## O arquivo SECURITY.md
```markdown
# Segurança
## Relatando Questões de Segurança
Por favor, não relate vulnerabilidades de segurança por meios públicos.

Em vez disso, reporte-as ao canal de segurança dos responsáveis pelo projeto.

Por favor, inclua as informações abaixo (tanto quanto puder fornecer) para nos ajudar a entender melhor a natureza e o escopo do possível problema:
- Tipo de problema (buffer overflow, injeção SQL, XSS, etc.)
- Caminhos completos dos arquivos fonte relacionados ao problema
- A localização do código-fonte afetado (tag/branch/commit ou URL direta)
- Qualquer configuração especial necessária para reproduzir o problema
- Instruções passo a passo para reproduzir o problema
- Código de prova de conceito ou exploit (se possível)
- Impacto do problema, incluindo como um atacante pode explorar o problema

## Idiomas Preferidos
Preferimos que todas as comunicações sejam em português.
```

---

## Regras de Documentação
- Todos os arquivos devem ser criados utilizando a codificação **UTF-8** para compatibilidade.
- Abaixo de cada seção e antes do início da próxima, inclua um link para voltar ao topo.
- Nunca customize cores no arquivo usando hexadecimal ou RGB(A), apenas adote os 140 possíveis "HTML Color Names".
- Escreva sempre em português brasileiro (PT-BR).
- Elimine qualquer linguagem emocional ou informal.
- Não use o caractere "—". Em seu lugar, onde fizer sentido semanticamente, use parênteses "()", ponto e vírgula ";" ou dois pontos ":".
- Mantenha tanto o código Markdown quanto o código HTML bem formatado, respeitando a indentação e a hierarquia de tags.
- Não use muitos emojis, somente onde realmente julgar necessário para chamar atenção ou para facilitar o entendimento.
- Só utilize links nas badges (project shields) onde for necessário ou solicitado.
- **Não use** `style=for-the-badge` nas badges.
