---
name: choosing-rubrics
description: Use when deciding how Minerva drills are scored, explaining a score, choosing rubrics for a scenario or preset, or mapping a contact center's QA form or scorecard to Minerva.
---

# Choosing rubrics

A rubric is what the judge scores after a call. Agents read rubrics; people build and edit them in the Minerva app. Read `docs_get rubrics` for the criterion types, weights and how the total is made.

## The default

Every workspace starts with **Customer call essentials**: Reached the outcome and Avoided the pitfalls (pass/fail, both judged against the scenario's expectations), No promises outside policy (pass/fail), Opening, Discovery, Empathy, Resolution, Objection handling and Close (scored), and Tone and pace (a note). Because the judge reads each scenario's expectations, it fits most calls; a new rubric earns its place when the floor scores something it lacks.

## Pick one

1. `rubrics_list`, then `rubrics_get` on the candidates.
2. Match each scenario's call type to the rubric whose criteria name what that call tests. Calls whose facts come out only when asked need a criterion that rewards questions (Discovery does).
3. Set it in the scenario's `rubricIds`, or in the preset's. A scenario with none is judged by the workspace default.

## Map a QA form

When the floor has its own QA form, write the mapping for the person to build in the app (Library, Rubrics):

| QA form line | Type | Weight | Guidance (what good looks like, or the pass condition) |
| --- | --- | --- | --- |

One row per line of the form. A must ("verifies identity") is pass/fail; a line rated on a scale is scored; a comments-only line is a note. Keep their wording, so scores read like their own form. Then point the scenarios and presets at the new rubric.

## Explain a score

`evaluations_get` on the drill gives each criterion's value, the judge's comment and the quoted evidence. Explain the score criterion by criterion from that evidence.
