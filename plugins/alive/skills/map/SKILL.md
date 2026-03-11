---
description: "Render an interactive map of your world. Generates the world index from all walnut and capsule frontmatter, then produces a force-directed graph showing connections between walnuts, people, capsules, and tags. Opens in the browser."
user-invocable: true
---

# Map

Visual overview of the entire ALIVE world — connections, clusters, health.

Not a list (that's the tree in alive:world). Not a search (that's alive:find). Map is spatial — it shows how everything connects and where the energy is.

---

## What It Does

### 1. Generate the World Index

Walk all walnuts. For each, read frontmatter from `_core/key.md` and `_core/_capsules/*/companion.md`.

**Backward compat:** If `_core/` doesn't exist, check walnut root for system files. If `_core/_capsules/` doesn't exist, fall back to scanning `_core/_working/` and `_core/_references/`.

Collected data per walnut:
- Name, type, goal, phase, health, rhythm, tags
- People (from `_core/key.md` `people:` field)
- Links (from `_core/key.md` `links:` field)
- Parent (from `_core/key.md` `parent:` field)
- Capsules (from `_core/_capsules/*/companion.md` frontmatter — name, status, goal)
- Last updated (from `_core/now.md` `updated:` field)

Write the index to `.alive/_index.yaml`:

```yaml
generated: 2026-03-12T14:30:00Z
version: 1.0
stats:
  walnuts: 14
  people: 23
  capsules: 31
  inputs: 2
  sessions: 47

walnuts:
  nova-station:
    type: venture
    goal: "Build the first civilian orbital tourism platform"
    domain: 04_Ventures
    phase: testing
    health: active
    rhythm: weekly
    updated: 2026-03-10
    tags: [space, tourism, engineering]
    people: [jax-stellara, dr-elara-voss, ryn-okata]
    links: [glass-cathedral, walnut-plugin]
    parent: null
    capsules:
      shielding-review: { status: draft, goal: "Evaluate radiation shielding vendors" }
      launch-checklist: { status: prototype, goal: "Pre-launch safety checklist" }
```

### 2. Render the Graph

Generate an interactive force-directed graph using D3.js. Write to `.alive/context-graph.html`.

**Nodes:**
- Walnuts (primary nodes — largest)
- People (medium nodes — connected to walnuts they appear in)
- Capsules (small nodes — nested under their walnut)
- Tags (tiny nodes — shared connections between walnuts)

**Edges:**
- `links:` field connections between walnuts
- `parent:` -> child relationships (thicker line)
- Person -> walnut connections (from `people:` field)
- `sources:` paths that cross capsule/walnut boundaries
- Shared tags (light, dotted)

**Color by ALIVE domain:**
- Life = green
- Ventures = blue
- Experiments = purple
- Archive = grey
- People = warm amber
- Inputs = orange

**Size by activity:**
- Recently saved (last 7 days) = larger
- Quiet (past rhythm) = normal
- Waiting = smaller, dimmer

**Health signals visible:**
- Active = bright, full opacity
- Quiet = 60% opacity
- Waiting = 40% opacity, warning border

### 3. Open in Browser

```
╭─ 🐿️ map generated
│
│  14 walnuts, 23 people, 31 capsules
│  3 clusters detected: space-ventures, personal-growth, creative-experiments
│
│  ▸ Opening in browser...
╰─
```

---

## Graph Features

### Interactive Controls

- **Click node** -> show `_core/key.md` frontmatter summary in a side panel (goal, phase, people, recent activity)
- **Hover** -> highlight all connected nodes and edges
- **Drag** -> reposition nodes (physics simulation)
- **Zoom + pan** -> navigate large worlds
- **Double-click walnut** -> expand to show its capsules as nested nodes

### Filters

- **By domain:** Toggle Life / Ventures / Experiments / Archive visibility
- **By tag:** Select a tag to highlight all walnuts sharing it
- **By health:** Show only active / quiet / waiting
- **By person:** Select a person to highlight their walnut connections
- **Search:** Type a name to find and focus on a specific node

### Layout Modes

- **Force-directed** (default) — organic clustering by connections
- **Domain-grouped** — arranged by ALIVE domain (Life left, Ventures center, Experiments right)
- **Timeline** — horizontal layout by last-updated date (most recent on right)

---

## Files

| File | Purpose |
|------|---------|
| `.alive/_index.yaml` | Generated world index — all frontmatter in one file |
| `.alive/context-graph.html` | Interactive D3.js graph — self-contained HTML |
| `.alive/scripts/generate-index.py` | Index generator script (if exists, run it; otherwise inline the logic) |

---

## Regeneration

The index and graph should be regenerated:
- On every `alive:map` invocation (always fresh)
- Suggested after `alive:save` when structural changes occurred (new walnut, new capsule, new person)
- After `alive:tidy` resolves issues that affect the graph (broken links, orphan walnuts)

```
╭─ 🐿️ world changed — regenerate map?
│  New walnut created: flux-engine
│  2 new capsules, 1 new person
│
│  ▸ Regenerate / Skip
╰─
```

---

## What Map Is NOT

- Not `alive:world` — world is the operational dashboard (what to work on). Map is the spatial view (how things connect).
- Not `alive:find` — find retrieves specific content. Map shows the topology.
- Not `alive:tidy` — tidy fixes structural issues. Map visualizes the structure.

World answers "what should I do?" Map answers "what does my world look like?"
