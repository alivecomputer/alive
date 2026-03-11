---
description: "The human has chosen a walnut to focus on. They're ready to work. Load its context, show what's changed, and get out of the way — loads core files in sequence, offers one unprompted observation before asking what to work on, and establishes single-walnut focus."
user-invocable: true
---

# Open

Single-walnut focus. Load one walnut. See where things are. Work.

---

## If No Walnut Named

Show available walnuts as a numbered list grouped by domain:

```
╭─ 🐿️ pick a walnut
│
│  Life
│   1. identity         active    Mars visa application
│   2. health           quiet     Sleep study results
│
│  Ventures
│   3. nova-station      active   Orbital test window
│   4. paper-lantern     quiet    Menu redesign
│
│  Experiments
│   5. midnight-frequency active  Episode 12 edit
│   6. glass-cathedral   waiting  Decide: gallery or festival
│
│  number to open, or name one.
╰─
```

## Load Sequence

Read in order (show `▸` reads):

1. `_core/key.md` — what this walnut is
2. `_core/now.md` — where it is right now
3. `_core/insights.md` — frontmatter scan (what domain knowledge exists)
4. `_core/tasks.md` — current task queue
5. `_core/_squirrels/` — any unsigned entries?
6. `_core/_capsules/` — **companion frontmatter only** (scan what capsules exist, their status and goal — don't read full companions)

**Backward compat:** Check `_core/` first for system files, fall back to walnut root. If `_core/_capsules/` doesn't exist, fall back to scanning `_core/_working/` and `_core/_references/` instead.

```
▸ _core/key.md       Nova Station — orbital tourism platform, weekly rhythm
▸ _core/now.md       Phase: testing. Capsule: shielding-review. Next: review telemetry.
▸ _core/insights.md     3 sections (engineering, regulatory, partners)
▸ _core/tasks.md        2 active, 1 urgent, 4 to do
▸ _core/_squirrels/  1 unsigned entry (empty — safe to clear)
▸ _core/_capsules/   3 capsules (shielding-review: draft, launch-checklist: prototype, safety-brief: done)
```

## The Spark

One observation the human might not have noticed. A connection, a question, a nudge.

```
╭─ 🐿️ spark
│  Ryn hasn't been mentioned in 8 days but there are 2 telemetry
│  reports from her team sitting in email. Might be test results.
╰─
```

If there's not enough context for a genuine spark, skip it. An obvious one is worse than none.

## Then Ask

```
╭─ 🐿️ nova-station
│  Goal:    Build the first civilian orbital tourism platform
│  Phase:   testing
│  Next:    Review telemetry from test window
│
│  Load full context, or just chat?
╰─
```

"Load context" reads log frontmatter, recent entries, linked walnuts.
"Just chat" starts freestyle — the squirrel loads more later if needed.

## During Work

- Stash in conversation (see squirrels.md). No file writes except capture + capsule work.
- Always watching: people updates, capsule progress, capturable content.
- When a capsule reaches prototype → offer to promote to published.

## Cross-Loading

If another walnut becomes relevant during work ("this references [[ryn-okata]]"), ask before loading it. One walnut, one focus.

```
╭─ 🐿️ cross-reference
│  This mentions [[ryn-okata]]. Load her context?
╰─
```

## Unsigned Entry Recovery

If `_core/_squirrels/` has an unsigned entry with stash items from a previous session:

```
╭─ 🐿️ previous session had 6 stash items that were never saved.
│  Review before we start?
╰─
```

If yes: present the previous stash for routing. If no: clear and move on.
