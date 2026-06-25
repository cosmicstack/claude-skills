# HTML Rendering — beautiful views of the model

The Markdown files are the source of truth. After a meaningful edit, **regenerate the matching HTML view** so the user has a polished, at-a-glance picture. HTML is a *derived build*: never hand-edit it, never treat it as canonical state.

Goals: **self-contained** (inline CSS, no build step, no external fetches except optional Google Fonts), **beautiful and calm** (a clean "intelligence dossier" aesthetic — elegant, not flashy), **prints well**, and **renders the model's semantics visually** rather than dumping the raw Markdown.

Four files live in the folder:

| File | Renders | Headline it shows |
|------|---------|-------------------|
| `index.html` | dashboard / cover | N people · M open questions · K branches |
| `world_model.html` | §1–§4 of `world_model.md` | the board |
| `open_questions.html` | `open_questions.md` | open vs. resolved |
| `counterfactuals.html` | `counterfactuals.md` | branch table + scenarios |

Every view shares the same `<head>` + CSS (below) and the same top nav, so the four feel like one document. The nav's `aria-current="page"` marks the active view.

---

## Semantic rendering rules (the part that matters)

Don't transcribe Markdown to `<p>` tags. Render *meaning*:

- **Observed vs. Inferred** → two visually distinct badges (`.badge.obs`, `.badge.inf`). Inferred is the warmer/softer color so the eye reads "this is a guess." This split is the skill's signature discipline; it must be unmissable in the HTML.
- **Flags** → chips. ⚠️ load-bearing inference = amber `.chip.load`; ✅ keystone = teal `.chip.keystone`. Put keystone chips on the person/relationship they mark.
- **Competing read** (the steelman of an antagonist) → its own `.callout.fork` under that person, labeled "Competing read," with the distinguisher called out. Never bury it.
- **Org chart** → the ASCII tree verbatim inside a `.tree` monospace card (preserve whitespace with `<pre>`). Don't try to redraw it as boxes.
- **People** → one `.person` card each; the user's own card gets a subtle "you" marker.
- **Synthesis** → three labeled callouts: `.callout.seam` (structural seams), `.callout.keystone` (the keystone), `.callout.unsolved` (what does NOT get solved). These are the payload — give them weight.
- **Open questions** → `.q.open` items (numbered, with a priority pill and the seam/branch each gates) and a separate `.q.resolved` section (struck-through prompt, the answer, the date).
- **Counterfactual branches** → the comparison `<table>`, then one `.scenario` card per developed branch with posture-vs-action and concentration risk made explicit.
- **Inference honesty** → anywhere the analysis hedges, keep the hedge visible (e.g. a small `.tentative` note). Don't let HTML polish harden a guess into a fact.

Keep a `.privacy` banner at the top of every view and a footer reminding the user this is their private working model and that they can ask the agent to update or simulate further.

---

## Shared `<head>` + CSS (inline this in every file)

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title><!-- Context — View --></title>
<style>
  :root{
    --ink:#1c2230; --ink-soft:#46506a; --paper:#f7f5f0; --card:#fffdf9;
    --line:#e2ddd2; --accent:#3a5a8c;            /* slate-blue, primary */
    --obs:#2f6b4f; --obs-bg:#e9f3ec;             /* observed = grounded green */
    --inf:#9a6b1f; --inf-bg:#f7efdd;             /* inferred = amber, "a read" */
    --load:#b4530a; --load-bg:#fbe7d6;           /* ⚠️ load-bearing */
    --key:#1f7a78;  --key-bg:#d9efee;            /* ✅ keystone */
    --risk:#a23b3b; --risk-bg:#f6e3e3;
  }
  *,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
  body{font-family:Georgia,'Iowan Old Style',serif;background:var(--paper);
    color:var(--ink);font-size:17px;line-height:1.7;padding:0 1.25rem 5rem;}
  .page{max-width:840px;margin:0 auto;}

  /* nav + privacy */
  .nav{display:flex;gap:.25rem;flex-wrap:wrap;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;
    font-size:12px;letter-spacing:.08em;text-transform:uppercase;
    padding:1.1rem 0;border-bottom:1px solid var(--line);position:sticky;top:0;background:var(--paper);z-index:5;}
  .nav a{color:var(--ink-soft);text-decoration:none;padding:.3rem .7rem;border-radius:999px;}
  .nav a:hover{background:var(--card);}
  .nav a[aria-current="page"]{background:var(--ink);color:var(--paper);}
  .privacy{font-family:-apple-system,sans-serif;font-size:11px;letter-spacing:.1em;
    text-transform:uppercase;color:#9a8f7a;margin:.9rem 0 0;}

  /* header */
  header.dossier{border-bottom:2px solid var(--ink);padding:1.4rem 0 1.6rem;margin-bottom:2.4rem;}
  .doc-label{font-family:-apple-system,sans-serif;font-size:12px;letter-spacing:.16em;
    text-transform:uppercase;color:var(--accent);font-weight:700;margin-bottom:.5rem;}
  h1{font-size:2rem;font-weight:normal;line-height:1.15;}
  .updated{font-style:italic;color:var(--ink-soft);font-size:.95rem;margin-top:.5rem;}

  h2{font-size:1.3rem;font-weight:bold;margin:2.6rem 0 .9rem;padding-left:.8rem;
    border-left:3px solid var(--accent);}
  h3{font-size:1.05rem;font-weight:bold;margin:1.5rem 0 .4rem;}
  p{margin-bottom:1rem;} ul,ol{margin:0 0 1rem 1.4rem;}
  a{color:var(--accent);}

  /* badges + chips */
  .badge{display:inline-block;font-family:-apple-system,sans-serif;font-size:10px;font-weight:700;
    letter-spacing:.1em;text-transform:uppercase;padding:.12rem .5rem;border-radius:4px;margin-right:.4rem;vertical-align:middle;}
  .badge.obs{color:var(--obs);background:var(--obs-bg);}
  .badge.inf{color:var(--inf);background:var(--inf-bg);}
  .chip{display:inline-block;font-family:-apple-system,sans-serif;font-size:11px;font-weight:600;
    padding:.15rem .55rem;border-radius:999px;margin:.15rem .3rem .15rem 0;}
  .chip.load{color:var(--load);background:var(--load-bg);}
  .chip.keystone{color:var(--key);background:var(--key-bg);}

  /* org tree */
  .tree{background:#fbfaf6;border:1px solid var(--line);border-radius:8px;padding:1rem 1.2rem;
    overflow-x:auto;box-shadow:0 1px 4px rgba(0,0,0,.05);}
  .tree pre{font-family:'SF Mono',ui-monospace,Menlo,monospace;font-size:13.5px;line-height:1.5;color:var(--ink);}

  /* person card */
  .person{background:var(--card);border:1px solid var(--line);border-radius:10px;
    padding:1.1rem 1.3rem;margin:1rem 0;box-shadow:0 1px 5px rgba(0,0,0,.05);}
  .person.you{border-left:4px solid var(--accent);}
  .person h3{margin-top:0;display:flex;align-items:center;gap:.5rem;}
  .person .role{font-weight:normal;font-style:italic;color:var(--ink-soft);font-size:.9rem;}
  .person .line{margin:.4rem 0;} .person .line .badge{margin-top:.1rem;}

  /* callouts */
  .callout{border-radius:0 8px 8px 0;padding:.9rem 1.2rem;margin:1.1rem 0;border-left:4px solid var(--accent);background:var(--card);}
  .callout .lbl{font-family:-apple-system,sans-serif;font-size:10px;font-weight:700;letter-spacing:.13em;
    text-transform:uppercase;margin-bottom:.4rem;display:block;}
  .callout.seam{border-color:var(--accent);} .callout.seam .lbl{color:var(--accent);}
  .callout.keystone{border-color:var(--key);background:var(--key-bg);} .callout.keystone .lbl{color:var(--key);}
  .callout.unsolved{border-color:var(--risk);background:var(--risk-bg);} .callout.unsolved .lbl{color:var(--risk);}
  .callout.fork{border-color:var(--inf);background:var(--inf-bg);} .callout.fork .lbl{color:var(--inf);}
  .tentative{font-size:.85rem;color:var(--ink-soft);font-style:italic;}

  /* open questions */
  .q{background:var(--card);border:1px solid var(--line);border-radius:8px;padding:.9rem 1.1rem;margin:.7rem 0;}
  .q .gates{font-size:.85rem;color:var(--ink-soft);}
  .pill{font-family:-apple-system,sans-serif;font-size:10px;font-weight:700;text-transform:uppercase;
    letter-spacing:.08em;padding:.1rem .5rem;border-radius:999px;}
  .pill.high{color:var(--risk);background:var(--risk-bg);} .pill.med{color:var(--inf);background:var(--inf-bg);}
  .pill.low{color:var(--ink-soft);background:#ece8df;}
  .q.resolved{opacity:.8;} .q.resolved .prompt{text-decoration:line-through;color:var(--ink-soft);}
  .q.resolved .answer{margin-top:.3rem;}

  /* branch table + scenarios */
  table{width:100%;border-collapse:collapse;margin:1.2rem 0;font-size:.95rem;background:var(--card);
    border:1px solid var(--line);border-radius:8px;overflow:hidden;}
  th{text-align:left;font-family:-apple-system,sans-serif;font-size:11px;letter-spacing:.06em;
    text-transform:uppercase;color:var(--ink-soft);background:#f1ede4;padding:.6rem .8rem;}
  td{padding:.65rem .8rem;border-top:1px solid var(--line);vertical-align:top;}
  td .risk{color:var(--risk);}
  .scenario{background:var(--card);border:1px solid var(--line);border-left:4px solid var(--accent);
    border-radius:0 10px 10px 0;padding:1.1rem 1.3rem;margin:1.2rem 0;box-shadow:0 1px 5px rgba(0,0,0,.05);}
  .scenario .pa{display:grid;grid-template-columns:auto 1fr;gap:.3rem .8rem;font-size:.93rem;margin:.6rem 0;}
  .scenario .pa b{color:var(--accent);}

  footer{margin-top:3.5rem;padding-top:1.2rem;border-top:1px solid var(--line);
    font-size:.9rem;color:var(--ink-soft);font-style:italic;}

  @media print{.nav{position:static;} body{background:#fff;} .person,.callout,.q,.scenario,.tree{box-shadow:none;}}
</style>
</head>
```

The shared body opens with the nav, privacy banner, and header:

```html
<body><div class="page">
  <nav class="nav">
    <a href="index.html">Overview</a>
    <a href="world_model.html" aria-current="page">The Board</a>
    <a href="open_questions.html">Open Questions</a>
    <a href="counterfactuals.html">Counterfactuals</a>
  </nav>
  <p class="privacy">● Private working model — your eyes only · not for circulation</p>
  <header class="dossier">
    <div class="doc-label">The Board</div>
    <h1><!-- Context name --></h1>
    <div class="updated">Last updated <!-- date --></div>
  </header>
  <!-- view body -->
  <footer>This is your private working model. Ask the agent to add a person, resolve a
    question, or war-game a new branch — and it'll update and re-render.</footer>
</div></body></html>
```

---

## Worked fragments

**A person card** (note the `.you` modifier on the user's own card):

```html
<div class="person">
  <h3>Priya <span class="role">— Design Manager (new)</span>
    <span class="chip load">⚠️ load-bearing read</span></h3>
  <div class="line"><span class="badge obs">Observed</span>Reorganized critique format
    week one; praised Marco publicly, not the user.</div>
  <div class="line"><span class="badge inf">Inferred</span>"Threatened by me, favoring Marco."
    <span class="tentative">— almost entirely inference.</span></div>
  <div class="callout fork"><span class="lbl">Competing read</span>
    New and managing up to Lena — amplifying whoever's work is easiest to showcase; would do
    this to anyone. <b>Distinguisher:</b> does she praise the user's work once it's review-ready, or never?</div>
</div>
```

**Synthesis callouts:**

```html
<div class="callout seam"><span class="lbl">Structural seam</span>Rating routes through a chain
  the user can't read (Priya→Lena); relevance routes through a roadmap they don't own (Tess/Aurora).</div>
<div class="callout keystone"><span class="lbl">✅ The keystone</span>Tess — ascending, already
  values the work, and her success metric is the one thing that makes the user indispensable through the reorg.</div>
<div class="callout unsolved"><span class="lbl">What does NOT get solved</span>Making work load-bearing
  for Tess routes <i>around</i> the Priya rating problem; it doesn't cure it. Concentration risk on one pod.</div>
```

**An open question and a resolved one:**

```html
<div class="q open"><span class="pill high">High</span> <b>2.</b> What is the user's real target?
  <div class="gates">Gates branches B and C — recognition vs. rating-safety.</div></div>

<div class="q resolved"><span class="prompt">Exposure to Tess?</span>
  <div class="answer"><b>Resolved:</b> direct and warm; Tess would advocate but serves Aurora first. <i>(2026-06-20)</i></div></div>
```

**A developed scenario** (posture vs. action made explicit):

```html
<div class="scenario"><h3>Developed: Branch B — make work load-bearing in Aurora</h3>
  <div class="pa"><b>Posture</b><span>Drop attachment-to-outcome, keep the conviction.</span>
    <b>Action</b><span>Bring strong critique points to Tess directly, before the meeting,
      framed as "what makes Aurora ship better."</span></div>
  <p><span class="badge obs">Risk</span><span class="risk">Concentration on Tess — if her pod is
    deprioritized, the protection goes with it.</span></p></div>
```

---

## `index.html` — the dashboard

A cover page: the context name, a one-line situation summary, and three big stat tiles (people · open questions · branches) that link to the three views. Below the tiles, surface the **keystone** and the **top open question** as a teaser so the overview is useful on its own, not just a menu. Same nav/CSS; `aria-current` on "Overview". Keep it to one screen.

## Generating and opening

- Write each HTML file with the Write tool; regenerate only the view(s) whose source changed (plus `index.html` when the headline counts move).
- After regenerating, offer to open it — macOS `open <folder>/index.html`, Linux `xdg-open`, Windows `start`. Don't auto-open every turn; open when the user would want to look.
- Keep escaping sane: HTML-escape user text (`&`, `<`, `>`); the ASCII org tree goes inside `<pre>` so whitespace survives.
