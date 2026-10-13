# Coordination — o "Jira + Swagger" do time

Esta pasta é o **ground truth** compartilhado entre os agentes. Tudo aqui é fonte única de verdade.

## Arquivos

| Arquivo | Quem escreve | Quem lê |
|---|---|---|
| `adr-<slug>.md` | architect | PM, devs |
| `research-report.md` | research | Manager, PM, architect |
| `prompt-strategy-<slug>.md` | prompt-engineer | architect, devs |
| `prompt-engineer-report.md` | prompt-engineer | Manager, architect |
| `spec.md` | PM | todos |
| `api-contract.yaml` | PM | backend-dev, python-dev, frontend-dev, qa-tester, reviewers |
| `types.ts` | PM | backend-dev, python-dev, frontend-dev |
| `architect-report.md` | architect | Manager, PM |
| `pm-report.md` | PM | Manager |
| `backend-dev-report.md` | backend-dev | Manager, QA, reviewers, scribe |
| `python-dev-report.md` | python-dev | Manager, QA, reviewers, scribe |
| `frontend-dev-report.md` | frontend-dev | Manager, QA, reviewers, scribe |
| `devops-dev-report.md` | devops-dev | Manager, QA, reviewers, scribe |
| `conversation-designer-report.md` | conversation-designer | Manager, QA, scribe |
| `code-review-report.md` | code-reviewer | Manager, QA, scribe |
| `security-review-report.md` | security-reviewer | Manager, QA, scribe |
| `qa-report.md` | qa-tester | Manager, scribe |
| `scribe-report.md` | scribe | Manager |

## Regra de ouro

Durante a Fase 2 (devs implementando em paralelo), **`api-contract.yaml` e `types.ts` são imutáveis**. Se um dev precisa mudar, ele volta ao Manager/PM — nunca edita sozinho. Isso evita que Front, Back e Python divirjam silenciosamente.

## Consulte o grafo primeiro

Antes de ler arquivos brutos do código, todo agente consulta `graphify-out/wiki/index.md` e `graphify-out/GRAPH_REPORT.md`. Só lê arquivo cru quando o grafo não responde.

## Ciclo de vida

1. (opcional) Architect escreve `adr-<slug>.md`.
2. PM escreve `spec.md`, `api-contract.yaml`, `types.ts`.
3. Devs rodam em paralelo (worktrees), leem contrato, implementam, escrevem seus `*-report.md`.
4. Manager revisa, faz merge dos worktrees.
5. Code-reviewer e Security-reviewer rodam em paralelo (read-only). Se alguém reprovar com severidade alta+, Manager despacha correção e repete.
6. QA roda, escreve `qa-report.md`.
7. Se REPROVADO: Manager despacha correção para o dev responsável, volta ao passo 3 (ou 4/5 se conseguir).
8. Se APROVADO: Scribe roda, grava aprendizados em `<VAULT>/`.
9. Arquive esta pasta (`coordination/done/<feature>/`) e comece a próxima.
