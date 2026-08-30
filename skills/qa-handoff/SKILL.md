---
name: qa-handoff
description: >-
  Monta o handoff para QA em comentário da Sub-task (e opcionalmente na
  descrição da PR): rotas HTTP, cenários, ambiente, pré-requisitos e evidência.
  Use com DELIVER-AGENT / DELIVER / QA-HANDOFF após EXECUTE com validation PASS.
---

# QA Handoff — Delivery Notes para QA

Gera um comentário **acionável para QA** na **Sub-task** do Jira (e, se pedido,
no body da PR). Foco: **o que testar** — especialmente **rotas** no backend.

## Quando usar

- Fluxo **DELIVER** / **DELIVER-AGENT** / **QA-HANDOFF**
- Após **EXECUTE** do TLC Spec Driven com `validation.md` PASS (ou aviso se
  ausente)
- Quando o time entrega uma Sub-task e o QA precisa saber rotas/cenários

## Entradas

| Entrada | Obrigatório | Uso |
|---------|-------------|-----|
| Key da Sub-task (ex.: `BRT-11`) | Sim | Comentário Jira + slug `.specs/` |
| Branch fonte | Sim (se abrir PR) | `createPullRequest` / `gh pr create` |
| `.specs/<slug>/spec.md` | Recomendado | ACs, contratos, rotas |
| `.specs/<slug>/validation.md` | Recomendado | Evidência PASS |
| Diff da branch vs base | Sim | Rotas novas/alteradas |
| OpenAPI/Swagger do repo | Se existir | Completar tabela de rotas |

**Slug:** key da Sub-task em minúsculas (`BRT-11` → `brt-11`).

## Como extrair rotas (ordem)

1. **Spec** — critérios de aceite / contratos HTTP em `.specs/<slug>/spec.md`
2. **Diff** — arquivos de rotas, controllers, OpenAPI alterados na branch
3. **Swagger/OpenAPI** no repo (se existir) — paths tocados pela US
4. Se ainda faltar rota óbvia no diff e não estiver na spec: listar como
   **gap** no handoff (“confirmar com DEV”) — **não inventar** path/método

Para cada rota, derive cenários a partir dos ACs (happy + erros 4xx citados
na spec). Sem AC de erro → pelo menos happy path + 1 erro óbvio se o diff
mostrar tratamento.

## Template — Comentário na US (Jira)

Use **markdown**. Título fixo para o QA achar fácil:

```markdown
## QA Handoff — <US-KEY>

**Feature:** <título curto da US>
**Branch:** `<branch>`
**PR:** <url ou "será criada após confirmação">
**Ambiente:** <ex.: API local `:3333` / staging URL>
**Validation:** <PASS — `.specs/<slug>/validation.md` | AUSENTE — avisar QA>

### O que foi entregue
- <3–6 bullets de produto/comportamento>

### Rotas a testar
| Método | Rota | Cenário | Resultado esperado |
|--------|------|---------|-------------------|
| GET | /exemplo | lista vazia/com dados | 200 + body conforme spec |
| POST | /exemplo | body válido | 201 |
| POST | /exemplo | <caso de erro da spec> | <status> |

### Pré-requisitos
- <migration/seed/auth/header/feature flag — ou "nenhum">

### Como verificar (rápido)
1. <passo>
2. <passo>
3. <passo>

### Fora de escopo nesta entrega
- <itens adiados / não cobertos>

### Evidência
- Spec: `.specs/<slug>/spec.md`
- Validation: `.specs/<slug>/validation.md` (<PASS/FAIL/ausente>)
- Commits: `<base>..<HEAD>` ou range curto
```

## Template — Descrição da PR (opcional)

Reutilize o mesmo bloco **QA Handoff** no body da PR, prefixado com:

```markdown
## Summary
- <1–3 bullets do que mudou>

## Test plan
- [ ] QA: seguir comentário **QA Handoff** na US <KEY>
- [ ] Gates locais: <comandos da tasks.md se existirem>
```

## Regras

- **1 US = 1 handoff** (não por task)
- Sempre incluir tabela **Rotas a testar** em entregas de API/backend
- Front-only: trocar a tabela por **telas/fluxos** + URLs; se chamar API,
  listar as rotas consumidas
- Não dump de arquivos nem narrativa de tasks
- Não abrir PR / não comentar no Jira sem confirmação do fluxo DELIVER
  (`AskQuestion`)
- Tom objetivo, em **português**
