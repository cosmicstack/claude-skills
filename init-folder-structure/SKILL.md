---
name: init-folder-structure
description: Initialize Krishanth's personal ~/Code folder structure on a new device or cloud environment. Creates the standard skeleton of top-level dirs and analysis subdirs, then guides selective project cloning. Use when setting up a new machine, cloud instance, or dev environment, or when the user says "init my code folder", "set up my dev environment", or "bootstrap my Code directory".
---

# Init Folder Structure

## Quick start

Run this one-liner to create the full skeleton:

```bash
mkdir -p ~/Code/{analysis/{ai,de,ds,ml},archive,learn,projects,research,sandbox}
```

That's it — the structure is ready. Now selectively clone or copy only the projects relevant to this environment.

## Full structure

```
~/Code/
├── analysis/
│   ├── ai/     # neural nets, deep learning, LLM systems
│   ├── de/     # data pipelines, ETL, orchestration
│   ├── ds/     # exploratory and statistical analysis
│   └── ml/     # model training, feature engineering, classical ML
├── archive/    # completed or inactive work — for reference, not active use
├── learn/      # structured study: books, courses, tutorials
├── projects/   # things built to run repeatedly: apps, pipelines, services
├── research/   # original investigation: literature maps, paper surveys, novel research gaps
└── sandbox/    # throwaway experiments — nothing here is meant to last
```

## Rules

- **Taxonomy is the constant; contents vary.** Not every environment needs every project.
- **Never improvise top-level dirs.** If something doesn't fit, revisit the taxonomy — don't create a one-off folder.
- **Clone selectively.** Only bring in what's relevant to this environment.

## Where things belong

| Work type | Folder |
|---|---|
| Answering a question / exploration | `analysis/ds/`, `analysis/ml/`, or `analysis/ai/` |
| Building something that runs repeatedly | `projects/` |
| Following a course, book, or tutorial | `learn/` |
| Original research: surveying papers, mapping a field, finding a novel gap | `research/` |
| Quick throwaway experiment | `sandbox/` |
| Done and no longer actively maintained | `archive/` |

**`learn/` vs `research/`:** `learn/` is consuming established, settled material (a course, a textbook). `research/` is producing new knowledge — reading the frontier literature to identify an open problem or stake out a novel contribution.

## ml/ vs ai/ distinction

Default rule: structured/tabular data → `ml/`. Neural architectures, embeddings, large pretrained models → `ai/`. When fuzzy, pick `ai/`.

## After the skeleton

1. Clone repos relevant to this environment (remotes are HTTPS and unaffected by local path).
2. Check IDE workspace files (`.idea/`, `.vscode/`) for hardcoded absolute paths if moving existing projects.
3. Verify `cd ~/Code/analysis/ds/` and other paths work — navigation should be identical to every other environment.
