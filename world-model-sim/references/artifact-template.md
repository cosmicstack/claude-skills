# Artifact Template — `world_model.md`

This is the canonical structure for the persisted world-model file. Create it on first build and edit it section-by-section thereafter. Each section header below explains *why it exists* — keep that intent when you maintain it.

Save to the working directory as `world_model.md`, or `<context>_world_model.md` if the user tracks more than one environment (e.g. `current_team_world_model.md`).

---

## Skeleton to instantiate

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

## 5. Open Questions
<Prioritized unknowns a counterfactual would turn on. Move resolved ones down.>
### ✅ Resolved
<Grows over time. Each entry: question → answer → date.>

## 6. Counterfactual Branches
| Branch | Target it serves | Core move | Main risk |
|--------|------------------|-----------|-----------|
| <A>    | <which goal>     | <action>  | <failure mode> |

### Developed: <chosen branch>
<War-gamed against concrete, named interactions. How each relevant person responds.
Posture vs. action made explicit. Concentration risk named.>
```

---

## Maintenance rules

- **Surgical edits.** Update the named section that changed; don't rewrite the whole file. The model is supposed to accrete.
- **Keep the split honest.** When new information arrives, file it under `[Observed]` or `[Inferred]` deliberately. If an inference gets confirmed by behavior, move it to `[Observed]` and note what confirmed it.
- **Resolve, don't delete.** When an open question is answered, move it to the `✅ Resolved` subsection with the answer — the history is useful.
- **Re-synthesize after big changes.** Adding a person or resolving a keystone unknown can change the seams. Revisit Section 4 when the board shifts.
- **Bump the date.** Update `Last updated` on every edit.
