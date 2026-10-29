---
name: building-presets
description: Use when giving a Minerva team ready drills, assigning practice to trainees, building a difficulty ladder, or after editing a persona, scenario or rubric that presets use.
---

# Building presets

A preset pins one persona, one scenario and its rubrics, so a trainee starts a drill with one tap. Read `docs_get presets` for the fields and who sees each kind.

## Which kind

- A team's assigned practice is `recommended`, with the team ids from `teams_list` in `teamIds`. Managers can assign only their own teams.
- The starters' own presets are `default`: edit them when useful; new presets are `recommended` or `saved`.
- Your own shortcuts are `saved`.

## Build a ladder

For each call type, order the presets from easy to hard and name them so the order shows ("1 · Internet down × older customer", "2 · …"). Run each scenario first with an easier persona, then a harder one: the same call at difficulty 2 and at 4 shows whether a trainee holds up under pressure. Tags group the presets by call type.

## Starter pairs

Each starter set comes with three default presets pairing its own personas and scenarios, all judged by "Customer call essentials":

- Customer service: Late order × rushed customer · Wrong items with an allergy × polite regular · Double charge × angry customer
- Technical support: Fibre outage × impatient power user · Wi-Fi down × patient novice · Payroll lockout × account owner on a deadline
- Sales: Cold call × busy salon owner · Quote follow-up × skeptical finance lead · Renewal with upgrade × undecided restaurant owner

They make a ready first rung; new pairs mix a starter scenario with your own personas, or the reverse.

## Re-pin after every edit

Saving a preset pins the **current** versions of its persona, scenario and rubrics. After any of them changes, `presets_get`, then `presets_save` with the same `id` and content, or trainees keep drilling the old version. `presets_list` with each kind finds the presets to re-save.

New: `presets_save` with no `id` and a fresh `idempotencyKey`.
