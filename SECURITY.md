# Política de Segurança (Security Policy)
Este repositório é um projeto exclusivamente educacional composto por arquivos de documentação (Markdown) com tutoriais e guias sobre o uso de **Inteligência Artificial**. Por não conter código-fonte executável, binários ou serviços em produção, o escopo de segurança é voltado à integridade do conteúdo informativo.

## Versões suportadas
Como se trata de uma base de conhecimento em constante atualização, apenas o conteúdo mais recente na branch principal (`main`) recebe revisões e correções.

## O que é considerado um problema de segurança?
- **Comandos danosos ou inseguros:** Instruções ou exemplos de comandos que possam expor credenciais, chaves SSH, tokens de API ou dados sensíveis sem o devido alerta.
- **Links maliciosos ou sequestro de domínios (Broken Link Hijacking):** Links externos na documentação que apontem para sites maliciosos, páginas de phishing ou domínios expirados.
- **Injeção de scripts / XSS:** Caso o leitor utilize visualizadores específicos de Markdown com renderização de HTML habilitada.

## Como reportar uma vulnerabilidade
Se você identificou uma falha ou risco de segurança neste repositório:
1. **Não abra uma Issue pública** imediatamente se a falha puder induzir leitores a riscos graves (como execução de scripts ou links maliciosos ativos).
2. Entre em contato por meio do **[formulário em meu website pessoal](https://vinici.us.com/#contact)**.
3. Inclua na mensagem:
   - Endereço do repositório;
   - O arquivo e a linha onde o problema foi encontrado;
   - Uma breve explicação do risco de segurança (ex: por que aquele comando ou link pode ser perigoso);
   - Sugestão de correção (opcional, mas muito bem-vinda).
