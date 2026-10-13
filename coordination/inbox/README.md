# Inbox — comunicação assíncrona entre agentes

Inspirado no padrão de mailbox do OpenClaude. Resolve o problema de agentes rodando em paralelo precisarem coordenar sem se bloquearem.

## Quando usar

Use o inbox quando, durante a Fase 2 (devs em paralelo em worktrees isolados), você (agente) precisa de algo de outro agente mas **não pode parar** o trabalho. Em vez de bloquear, você deixa uma mensagem e segue avançando no que dá pra avançar.

Exemplos típicos:
- Frontend pergunta ao backend: "Qual o shape do erro 401?"
- Backend pergunta ao frontend: "Vou retornar `created_at` em ISO 8601, ok?"
- Qualquer agente pergunta ao Manager: "Spec diz X mas API contract diz Y — qual vale?"

**Não use inbox para coisas urgentes que bloqueiam totalmente seu trabalho** — nesse caso, falhe rápido com `status: needs-input` no relatório final e deixe o Manager despachar a próxima rodada.

## Formato do arquivo

Nome: `<from>-to-<to>-<feature>-<n>.md`

Exemplo: `frontend-dev-to-backend-dev-login-magic-link-001.md`

Conteúdo:

```markdown
---
from: frontend-dev
to: backend-dev          # ou: manager, pm, qa-tester
feature: login-magic-link
status: open             # open | answered | closed
priority: low            # low | normal | high
date: 2026-04-18
---

## Pergunta
<Direto ao ponto. Inclua contexto suficiente pra o destinatário responder sem precisar caçar arquivo.>

## Contexto
<Opcional: links pra arquivos/linhas específicas, exemplo de payload, etc.>

## Por que não bloqueio
<O que você está fazendo enquanto espera resposta. Ajuda o destinatário a saber a urgência real.>

## Resposta
<Vazio quando criado. O destinatário preenche aqui ao responder e muda status para answered.>
```

## Protocolo

1. **Criar mensagem**: agente A escreve arquivo seguindo o formato. `status: open`.
2. **Continuar trabalhando**: A não para. Avança no que dá (mocks, próxima tela, etc.).
3. **Verificar inbox**: antes de finalizar seu relatório, **todo agente lê o inbox** e responde mensagens com `to: <seu-papel>` e `status: open`. Para responder, edite o arquivo, preencha "Resposta" e mude `status: answered`.
4. **Manager monitora**: o Manager checa inbox antes de fechar a feature. Mensagens com `status: open` não respondidas são bloqueios.
5. **Fechar**: quando a resposta resolve a questão, o autor original muda `status: closed` (opcional — `answered` já basta para o Manager saber).

## Quando algo é "para o Manager"

Mensagens com `to: manager` aparecem na sua próxima revisão de inbox. Trate como bloqueio — não feche a feature sem respondê-las (ou escalar pro usuário se for decisão de produto).

## Limpeza

Mensagens viram histórico da feature. Quando a feature fecha, o Manager move o conteúdo do inbox para `coordination/done/<feature>/inbox/` (junto com os reports e a spec). Inbox raiz fica sempre limpo para a próxima feature.
