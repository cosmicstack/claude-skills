# Artifact Template — the `world_model/` folder

The model is a **per-context folder** of three Markdown source files (plus generated HTML — see [html-rendering.md](html-rendering.md)). Create the files as content arrives and edit them section-by-section thereafter. Each section header below explains *why it exists* — keep that intent when you maintain it.

Save to the working directory as `world_model/`, or `<context>_world_model/` if the user tracks more than one environment (e.g. `current_team_world_model/`).

```
<context>_world_model/
├── world_model.md         # §1 Structure, §2 People, §3 Dynamics, §4 Synthesis
├── open_questions.md      # prioritized unknowns + ✅ Resolved log
├── counterfactuals.md     # branch table + developed scenarios
└── *.html                 # generated views (do not hand-edit)
```

The three files cross-reference each other: synthesis seams in `world_model.md` motivate questions in `open_questions.md`, which gate the branches in `counterfactuals.md`. Keep them coherent — when one shifts, check whether the others need a touch.

---

## File 1 — `world_model.md`

```markdown
# World Model — <context name>
> Reading convention: [Observed] = visible behavior/fact, attributable to evidence.
> [Inferred] = the user's read on motive/intent. Flags: ⚠️ load-bearing inference,
> ✅ keystone (high-leverage node/relationship).
> Last updated: <date>

## 1. Org / Entity Structure
<ASCII trees. Reporting lines (solid), support/influence lines (dotted), matrixed
relationships called out. Capture this BEFORE people — structure constrains everything.>

## 2. People
### <Name / role>  (use a stable handle, e.g. initials or role)
- [Observed] <behaviors, stated facts, things visible to others>
- [Inferred] <the user's read on motive — flagged as inference>
- Flags: <⚠️ where an inference is load-bearing; ✅ where the relationship is keystone>
- Competing read: <for any antagonist, the benign hypothesis and what would distinguish it>

### <next person…>   (include the USER as one of the people)

## 3. Dynamics of Note
- <Reorgs, historical patterns, decision model (centralized/federated), live proposals,
  structural tensions.>
- Action stances: <what the user is currently DOING about each — and ⚠️ where a stance
  spends someone else's capital.>

## 4. Strategic Synthesis
- **Structural seams:** <the misalignments — roll the per-person detail up into a few
  structural facts. The "two misaligned chains" kind of statement.>
- **The keystone:** <the single highest-leverage node/relationship, and why.>
- **What does NOT get solved:** <residual risks, concentration risk, what a move
  routes-around vs. actually cures.>
```

## File 2 — `open_questions.md`

```markdown
# Open Questions — <context name>
> The specific unknowns a counterfactual would turn on. Prioritized. Resolve the top
> few with the user before simulating; don't force premature resolution of a fuzzy target.
> Last updated: <date>

## Open
1. <question> — why it matters: <which seam / branch it gates>. Priority: <high/med/low>.
2. …

## ✅ Resolved
<Grows over time. Each entry: question → answer → date. Don't delete resolved questions —
the history of what was learned is useful and feeds re-synthesis.>
- <question> → <answer> (<date>)
```

## File 3 — `counterfactuals.md`

```markdown
# Counterfactual Branches — <context name>
> Branches must lead to *different outcomes*, not just different tones. Each serves a
> target; each names its main risk. Internal-state shifts are postures — pair them with
> the structural move they enable.
> Last updated: <date>

## Branch table
| Branch | Target it serves | Core move | Main risk |
|--------|------------------|-----------|-----------|
| <A>    | <which goal>     | <action>  | <failure mode> |

## Developed: <chosen branch>
<War-gamed against concrete, named interactions ("the next time [person] walks in
with their plan…"). How each relevant person on the board responds. Posture vs. action
made explicit. Concentration risk and route-around-vs-cure named.>

## Archive
<Branches considered and set aside, with one line on why — useful when the board shifts
and an old branch becomes live again.>
```

---

## Maintenance rules

- **Surgical edits.** Update the named section in the right file; don't rewrite the whole file. The model is supposed to accrete.
- **Right file for the content.** People/structure/dynamics/synthesis → `world_model.md`. Unknowns → `open_questions.md`. Simulated moves → `counterfactuals.md`.
- **Keep the split honest.** When new information arrives, file it under `[Observed]` or `[Inferred]` deliberately. If an inference gets confirmed by behavior, move it to `[Observed]` and note what confirmed it.
- **Resolve, don't delete.** When an open question is answered, move it to `✅ Resolved` with the answer — the history is useful.
- **Re-synthesize after big changes.** Adding a person or resolving a keystone unknown can change the seams *and* can open or close branches. Revisit §4 in `world_model.md` and the branch table in `counterfactuals.md` when the board shifts.
- **Bump the date.** Update `Last updated` in every file you touch.
- **Re-render.** After editing a Markdown file, regenerate its HTML companion (and `index.html` if the headline counts changed). See [html-rendering.md](html-rendering.md).
