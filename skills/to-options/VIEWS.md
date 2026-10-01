# Views for questions that aren't UI

Lead with **output**: what a person actually gets under each option, with real-looking data. The JSON, the rows, the email, the alert. Then add at most one view of how it gets there, from the menu below.

Adapted from Dex Horthy's `show-me` (credited in `SKILL.md`).

## Menu

- **Pseudocode** for a rule:

```text
canRefillOnline(rx)
  if rx is controlled
    return no
```

- **Call tree** for what runs, in what order:

```text
partner GET /slots
  read the copy
refreshJob  every 60 s
  ScheduleClient.getOpenSlots
```

- **File tree** for where things live. Keep it shallow, one comment per line.
- **Sequence diagram** (Mermaid) for who talks to whom. Load Mermaid from `cdn.jsdelivr.net/npm/mermaid`.
- **Diff against today's shape** when the shape exists and the options change only part of it. This is the best side-by-side view: every option's diff against the same base. Match the diff to the topic (call tree, file tree, rule) and colour the `+` and `-` lines.

```diff
 bookingSite.showTimes
   ScheduleClient.getOpenSlots
+partner GET /slots
+  read the copy
```

- **Whole block** when most of it is new, or the decider needs the full target shape.

Use one or two of these per question, never the whole menu.
