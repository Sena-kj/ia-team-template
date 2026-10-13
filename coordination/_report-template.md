---
status: completed         # completed | failed | needs-input
agent: <role>             # pm | backend-dev | frontend-dev | qa-tester
feature: <feature-slug>   # ex: login-magic-link
date: 2026-04-18          # YYYY-MM-DD
# verdict: approved        # SÓ para qa-tester: approved | rejected
---

## Summary
<2-5 linhas. O Manager lê isso primeiro pra decidir o próximo passo. Direto ao ponto.>

## Result
<O que foi entregue. Estrutura varia por agente — ver instruções no agente:
- pm: lista de arquivos em coordination/ criados/atualizados
- backend-dev: endpoints implementados, branch/worktree, comando pra rodar local, migrations
- frontend-dev: telas/componentes, rotas, branch/worktree, comando pra rodar local, descrição do fluxo
- qa-tester: checklist de critérios, bugs (com severidade/passos/evidência), edge cases, regressões
- code-reviewer / security-reviewer: achados no formato `[SEVERIDADE · confiança alta|média|baixa]`.
  Severidade e confiança são campos INDEPENDENTES. Achado de confiança baixa entra no report
  com a ressalva escrita — nunca é omitido. Curadoria é do Manager, não do reviewer.>

## Next steps
- [ ] <ações concretas que o Manager precisa disparar a seguir>
- [ ] ...

## Dead-ends & detours
<Obrigatório se você tentou caminho X e virou pra Y. Uma linha por tentativa:
- **Tentei:** <abordagem X> → **Problema:** <por que não deu> → **Virei pra:** <abordagem Y>

Exemplos do que é valioso registrar:
- API/método que parecia servir mas tem limitação escondida
- Pattern do vault que falhou nesse contexto específico
- Bug do framework/lib que contornei de modo não-óbvio
- Decisão revertida mid-task e porquê

Isso alimenta o vault de learnings — um "não faça X aqui" ajuda o próximo agente tanto quanto um "faça Y".

Vazio se a implementação foi linha reta.>

## Blockers / questions
<Vazio se não houver. Caso contrário, liste ambiguidades, decisões pendentes, mensagens no inbox aguardando resposta. Se houver bloqueio que precisa do usuário, marque "→ requer humano".>
