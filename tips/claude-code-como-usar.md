---
title: Claude Code - Como Usar
category: tips
target_model: Claude Code
---
# Como Usar o Claude Code
Manual prático de comandos, permissões e operação do assistente de codificação de terminal Claude Code.

| Recurso | Descrição e Prompts Iniciais | Dicas e Erros Comuns |
|:--------|:-----------------------------|:---------------------|
| **📄 CLAUDE.md** | O arquivo de regras do seu projeto. O Claude o lê antes de cada tarefa. | 🔴 **Dica profissional:** Rode o linter em cada novo repositório antes do seu primeiro prompt.<br><br>⚠️ **Erro comum:** Escrever um romance. O Claude ignora arquivos longos. Seja específico e conciso. |
| **⚙️ Plan Mode** | Peça ao Claude para planejar antes de codificar.<br><br>**Exemplo:** "Planeje como você implementaria X. Não escreva código ainda." | 🔴 **Dica profissional:** Revise o plano, corrija a abordagem e SÓ ENTÃO diga "implemente isso".<br><br>⚠️ **Erro comum:** Deixar o Claude pular direto para o código. Ele escreve mais rápido do que pensa. |
| **🧪 TDD Loop** | Escreva um teste que falha. Passe para o Claude. Deixe-o implementar até o teste ficar verde. | 🔴 **Dica profissional:** Testes são a sua especificação. O Claude não tem como interpretar mal um teste vermelho.<br><br>⚠️ **Erro comum:** Não usar testes e depois se surpreender quando a implementação não corresponde ao que você queria. |
| **🌿 Git Worktrees** | Uma worktree por funcionalidade. Rode sessões separadas do Claude em branches separadas ao mesmo tempo. | 🔴 **Dica profissional:** Chega de usar stash. Chega de trocar de branch. Cada agente ganha seu próprio diretório de trabalho.<br><br>⚠️ **Erro comum:** Rodar tudo em uma única branch. Worktrees permitem que você paralelize o trabalho. |
| **📦 /compact** | Comprime o histórico da conversa para liberar espaço na janela de contexto. | 🔴 **Dica profissional:** Use antes do Claude começar a ficar lento. Inicie sessões limpas para novas tarefas.<br><br>⚠️ **Erro comum:** Uma mega-sessão para tudo. A poluição do contexto destrói a qualidade da resposta. |
| **💰 /cost** | Mostra o uso de tokens e o custo da sessão atual. | 🔴 **Dica profissional:** Verifique após tarefas grandes. Ajuda a entender o que está consumindo seus tokens.<br><br>⚠️ **Erro comum:** Nunca verificar. Você fica voando às cegas em relação aos gastos e ao uso de contexto. |
| **🤖 Subagents** | Cria agentes em segundo plano que trabalham em paralelo em tarefas separadas. | 🔴 **Dica profissional:** Use subagentes para tarefas independentes. Revisão de código + implementação ao mesmo tempo.<br><br>⚠️ **Erro comum:** Fazer tudo sequencialmente. O Claude pode rodar múltiplas tarefas em paralelo. |
| **📜 Skills** | Modelos de prompts reutilizáveis que seu time compartilha. Defina fluxos de trabalho como markdown em `.claude/skills/`. | 🔴 **Dica profissional:** Codifique padrões de revisão de código, checklists de deploy ou padrões de migração.<br><br>⚠️ **Erro comum:** Cada desenvolvedor criar prompts de forma diferente. Skills padronizam como seu time usa o Claude. |
