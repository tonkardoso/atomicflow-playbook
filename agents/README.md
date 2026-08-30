# Agentes do harness BRT — ordem dos passos

Este repositório é instalado como **submódulo** no path `.cursor` do repo do
produto. Skills ensinam o *como*; rules travam a *ordem*; agents são os *passos*.

| Ordem | Invocar | Arquivo | O que faz |
|------:|---------|---------|-----------|
| 1 | `PO-AGENT` | `PO-AGENT.md` | Criar / refinar US, bug, backlog (épico/sprint/prioridade) |
| 2 | `TECHLEAD-AGENT` | `TECHLEAD-AGENT.md` | US → 1 Sub-task técnica (Codegraph + Grill Me + assignee opcional) |
| 3 | `DEV-AGENT` | `DEV-AGENT.md` | Spec Driven na Sub-task: Discuss → Spec → Design → Tasks → Execute (+ Validation) |
| 4 | `DELIVER` | `DELIVER-AGENT.md` | QA Handoff na Sub-task + opcional PR |
| 5 | `PR-REMEDIATE` | `PR-REMEDIATE-AGENT.md` | Triagem CodeAnt → fix com confirmação |
| — | `TEACHER-TON` | `TEACHER-TON.md` | Mini-curso passo a passo de qualquer agente (onboarding do time) |

Handoff entre agentes é **manual** (o usuário invoca o próximo).

Para treinar o time: invoque `TEACHER-TON` — ele pergunta qual agente explicar
e avança step a step com confirmação.

## Artefatos no repo do produto

```
.specs/<slug-da-subtask>/
```

Slug = key da Sub-task em minúsculas.

## Templates (neste playbook)

- `.cursor/template/open-spec-us.md`
- `.cursor/template/open-spec-task.md`
