# BRT Agents Playbook

User harness compartilhado para o time: agentes Cursor + skills + rules +
templates Open Spec. Instalado como **git submodule** no path `.cursor` de cada
repositório de produto.

## Cadeia

```
PO-AGENT → TECHLEAD-AGENT → DEV-AGENT → DELIVER → PR-REMEDIATE
```

| Agente | Invocar | Papel |
|--------|---------|--------|
| PO | `PO-AGENT` | US / bug / refine / backlog (épico, sprint, prioridade) |
| Tech Lead | `TECHLEAD-AGENT` | 1 Sub-task técnica por US (Codegraph + Grill Me) |
| Dev | `DEV-AGENT` | Discuss → Spec → Design → Tasks → Execute (+ Validation auto) |
| Deliver | `DELIVER` | QA Handoff na Sub-task ± PR |
| PR Remediate | `PR-REMEDIATE` | CodeAnt → fixes com confirmação |
| Teacher | `TEACHER-TON` | Mini-curso passo a passo de todos os agentes |

Handoff entre agentes é **manual**.

## Layout deste repo (vira `.cursor/` no host)

```
agents/           # definições dos agentes
skills/           # tlc-spec-driven, grill-me, grilling, ponytail*, qa-handoff, …
rules/            # travas de ordem / AskQuestion / ponytail
template/         # open-spec-us.md, open-spec-task.md (PT)
README.md
```

## Artefatos no repo do **produto** (não neste playbook)

```
.specs/<slug-da-subtask>/
  context.md
  spec.md
  design.md
  tasks.md
  validation.md
```

Slug = key da Sub-task Jira em minúsculas.

## Instalação no repo host

Na raiz do repositório de produto (sem pasta `.cursor` pré-existente, ou
renomeie a antiga):

```bash
git submodule add <URL-deste-repo> .cursor
git submodule update --init --recursive
```

Se o host **já tem** `.cursor/`:

1. Mova o conteúdo antigo para backup.
2. Adicione o submodule em `.cursor`.
3. Reaplique customizações locais do host **fora** do submodule, se necessário.

Atualizar o playbook em todos os clones:

```bash
git submodule update --remote .cursor
```

## Pré-requisitos no Cursor do DEV

- Agent mode para fluxos com AskQuestion / Jira / PR
- MCP Atlassian/Jira
- MCP Codegraph (`user-codegraph`) — indexar o produto com `codegraph init` quando possível
- MCP Bitbucket e/ou `gh` (Deliver / PR-Remediate)

## Skills incluídas

- `tlc-spec-driven` — Spec Driven (+ **Ponytail obrigatório no Execute**)
- `grill-me` / `grilling`
- `ponytail` (+ audit, debt, gain, help, review)
- `qa-handoff`, `pr-remediate`, `learnings`, `find-skills`

## Fluxo resumido

1. **PO** grava a Story (Open Spec US).
2. **Tech Lead** (com o repo aberto) cria **uma** Sub-task (Open Spec TASK), assignee opcional.
3. **Dev** roda Spec Driven na Sub-task; Validation roda ao fim do Execute.
4. **Deliver** comenta handoff na Sub-task e/ou abre PR.
5. **PR-Remediate** trata CodeAnt com confirmação humana.

## Convenções

- 1 US → 1 Sub-task Jira; breakdown fino fica em `.specs/<slug>/tasks.md`
- Codegraph antes de Grep; Grep amplo proibido quando houver índice
- Nunca commit/push/PR sem confirmação nos fluxos Deliver / PR-Remediate
