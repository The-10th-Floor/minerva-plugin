---
name: writing-scenarios
description: Use when creating or editing a Minerva call scenario, picking a starter call, adding facts a customer reveals only when asked, or deciding what the judge should expect from a good call.
---

# Writing scenarios

A scenario is **one call**: `instructions` tell the customer what happened and how to behave, `expectations` tell the judge what a good outcome is. Read `docs_get scenarios` first: it holds the fields, the instruction blocks (SITUATION, FACTS, DO IN ORDER, REACTIONS, HIDDEN TRUTH, HOW IT ENDS), this workspace's call length and a worked example. Write to those blocks.

## Start from a starter

Adapt the closest starter before writing from scratch. The nine starter calls and what each tests are in [starters.md](starters.md). Two of them are annotated part by part, with why each part is there, in [examples.md](examples.md).

## Neutral and unpaired

Any persona can play any scenario, and the preset is where a pair is chosen (`building-presets`). So a scenario names no persona, and it is written in neutral language: no dialect, nationality, currency or city. The persona supplies the voice and says the quoted lines in its own words (`writing-personas`).

## What makes a scenario work

- **Facts are earned.** Each FACTS bullet ends with the question that reveals it, in parentheses: "The router's red light has been on since Tuesday (asked what the lights show)." These are what separate a probing agent from a scripted one.
- **The hidden truth is the customer's own**: something they know, did or want and never volunteer (they unplugged the router to move it; they plan to cancel anyway). A cause on the company's side that the customer cannot know, such as an area outage or a pending authorization, goes in `expectations`, where the judge checks the agent found it.
- **One complication per scenario.** A variant is a second scenario.
- **Real values**: order numbers, amounts, times, speeds.
- **Expectations describe results**: what must be true when the call ends, the failure case named, two or three pitfalls. When the right answer is a refusal, say so.

## Check, then save

Before each save: no persona, dialect, nationality, currency or city in the text; every fact has its revealing question; the hidden truth is something the customer knows; company-side causes sit in `expectations`.

- New: `scenarios_save` with no `id` and a fresh `idempotencyKey`. `rubricIds` picks the rubrics (`choosing-rubrics`).
- Edit: `scenarios_get`, change, then `scenarios_save` with the same `id` and the full content.
- Then re-save the presets that pin it (`building-presets`).
