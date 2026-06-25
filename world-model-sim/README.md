# world-model-sim

A Claude skill for thinking through sociopolitical environments — workplaces, orgs, communities, any multi-agent setting — by building a **persistent, structured model of the board** and running **counterfactual simulations** against it. Instead of generic "office politics" advice, it reasons about *your* specific people and forces: "what happens if I do X / stop doing Y / this reorg lands / I drop this stance."

## What it does

- Builds a Markdown **world model** of the people, teams, reporting lines, and dynamics around you.
- Keeps a disciplined split between what people **do** (observed) and **why** you think they do it (inferred) — because motive is where you're least certain and where scenarios turn.
- Synthesizes the per-person detail into **structural seams**, a **keystone** (the highest-leverage relationship), and an honest list of what a given move *won't* fix.
- Runs **counterfactual branches** and pressure-tests them against concrete, named interactions.
- Is **stateful**: the model is a file you grow over weeks. Each session reads it, updates it surgically, and leaves it richer.

## Install

Copy the `world-model-sim/` folder into your skills directory:

```
~/.claude/skills/world-model-sim/      # personal
# or
.claude/skills/world-model-sim/        # per-project
```

Claude loads it automatically and triggers it when a request is in scope.

## Usage

Just describe the situation. Triggering phrasings include:

- "I keep clashing with my new manager and there's a reorg coming."
- "How do I handle my skip-level?"
- "Should I push back harder, stay, or move?"
- "War-game what happens if I stop arguing in every meeting."
- "Continue my world model — I learned my skip actually does rate me." *(stateful update)*

You don't need to say "world model" or "counterfactual."

The skill writes your model to `world_model.md` (or `<context>_world_model.md`) in the working directory.

## Privacy

Your model will contain candid, sensitive characterizations of real, named people. **Keep it local and private.** A `.gitignore` ships with this skill that excludes `*world_model*.md` so you can't accidentally commit one. Don't share the file.

## Layout

```
world-model-sim/
├── SKILL.md                        # phased flow, principles, statefulness rules
├── README.md
├── .gitignore                      # ignores generated *world_model*.md
└── references/
    ├── artifact-template.md        # the world-model file structure
    ├── reasoning-principles.md     # the reasoning that makes it non-generic
    └── example-walkthrough.md      # a synthetic end-to-end session
```

All examples in this skill are **synthetic**.

## What it won't do

It's a thinking partner for navigating well and reaching good outcomes — not a tool for manipulating, sabotaging, or surveilling people. It will decline if a session turns that way.
