---
name: learnings
description: >-
  Grava aprendizados de PR/CodeAnt e convenções do projeto em .specs/. Use após
  remediação aprovada no PR-REMEDIATE ou quando o DEV documentar decisão sobre
  feedback de review.
---

# Learnings — Memória de PR e CodeAnt

Persiste o que o time aprendeu com review automatizada para **não repetir** o
mesmo comentário na próxima Sub-task.

## Quando gravar

- DEV aprovou fix no **PR-REMEDIATE** (commit ou decisão explícita)
- DEV pediu documentar alerta de spec (mesmo sem fix)
- Mesmo padrão do CodeAnt aparece **2+ vezes** → promover para convenção global

**Não grave** antes da decisão do DEV. **Não grave** opiniões vagas sem ação.

## Onde gravar

### Por Sub-task — `.specs/<slug>/learnings.md`

Slug = key da Sub-task em minúsculas (`BRT-11` → `brt-11`).

Crie o arquivo na **primeira** entrada. Append-only por sessão de remediação.

### Global — `.specs/conventions.md`

Use quando o aprendizado for **regra do projeto**, não detalhe de uma Sub-task:

- Padrão que o CodeAnt cobra repetidamente
- Decisão explícita do time (DTO, paginação, camadas, testes mínimos)

Se o arquivo não existir, crie com cabeçalho abaixo.

## Template — learnings.md (por Sub-task)

```markdown
# Learnings — <SUBTASK-KEY>

Registro de feedback de PR/CodeAnt e decisões desta Sub-task.

## <YYYY-MM-DD> — PR <link ou ID>

| Status | Comentário CodeAnt | Decisão / fix | Aprendizado |
|--------|-------------------|---------------|-------------|
| resolvido | … | … | … |
| alerta | … | manter spec; não aplicar | … |
| dismiss | … | comentário inválido | … |
```

## Template — conventions.md (global)

```markdown
# Convenções do projeto

Padrões acordados (origem: CodeAnt, review, spec). SPEC/TASKS/EXECUTE e
PR-REMEDIATE devem considerar este arquivo.

## <Área — ex.: API, Frontend, Testes>

- <regra acionável em uma linha> *(origem: CodeAnt / PR #N / SUBTASK-KEY)*
```

## Regras de redação

- **Uma linha acionável** por aprendizado — regra que a próxima feature aplica
- Escreva a **regra geral**, não o incidente
  - ✅ `Listagens públicas devem usar paginação no repository`
  - ❌ `CodeAnt reclamou na linha 88 do OrderController`
- **Status** claro: `resolvido`, `alerta`, `dismiss`, `pendente`
- Para **alerta de spec**, cite trecho da spec e o pedido do CodeAnt

## Leitura obrigatória em fluxos futuros

| Fluxo | Quando ler |
|-------|------------|
| DEV-AGENT — Spec/Design/Tasks | Início da etapa |
| PR-REMEDIATE | Antes de classificar comentários |
| DEV-AGENT — Execute | Ao montar plano de implementação |

Arquivos: `.specs/conventions.md` + `.specs/<slug>/learnings.md` (se existir).

## Relação com TLC lessons.json

O TLC Spec Driven usa `.specs/lessons.json` / `LESSONS.md` para falhas de
**verificação na EXECUTE**. Este skill cobre feedback de **PR/CodeAnt** — são
camadas complementares. Não misture entradas; se a mesma regra aparecer nos
dois lugares, prefira **conventions.md** como fonte humana legível.

## Exemplo de entrada

```markdown
| resolvido | Extrair validação duplicada | Movido para `validateOrderInput` | Validar input em helper reutilizável, não em cada controller |
```

Promover para `conventions.md` quando a coluna "Aprendizado" se repetir em
USs diferentes.
