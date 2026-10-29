---
name: writing-personas
description: Use when creating, editing or tuning a Minerva AI customer (a persona), picking a starter customer, or making a simulated caller harder, calmer, more talkative or quicker to escalate.
---

# Writing personas

A persona is who the AI customer is on **every** call: controls the platform reads, plus a free-text body. What happens on one call belongs to a scenario (`writing-scenarios`). Read `docs_get personas` first: the fields, the dialects this workspace serves, and a worked example.

## Start from a starter

Adapt the closest starter before writing from scratch. The nine starters, with their controls and what each practices, are in [starters.md](starters.md). Two of them are annotated part by part, with why each part is there, in [examples.md](examples.md).

A good library mixes routine, characterful, uncommon and stress customers. A stress case is a hard conversation, never an absurd request.

## Pick the dialect

`language` and `lexicon` come only from the pairs `docs_get personas` lists. Map the caller to the nearest listed pair: a caller from Saudi Arabia, the UAE, Kuwait or Qatar speaks Gulf Arabic; one from Jordan, Palestine or Syria speaks Jordanian. The customer keeps that one dialect from the first word to the last. Tell the person when the brief's dialect maps to a nearer listed one.

## Tune the behavior

Controls are rolled, voiced or compared across drills; everything else is the body.

| To change | Use |
| --- | --- |
| How hard they are to win over | `difficulty`. At 4 and 5, tone and confidence alone never move them; they need relevance and proof |
| Patience, doubt, chattiness, courtesy, firmness | `advanced.traits`, or `random` for variety across drills |
| The emotional baseline the voice keeps | `advanced.mood` |
| Cutting in | `advanced.interruption` |
| When they ask for a manager | `advanced.escalationThreshold` |
| Voice, avatar, age | `gender` and `ageRanges`; `random` or several ranges roll a new look each drill |
| How they talk, what wins them, what annoys them | The body, as observable patterns in their dialect's own words |

## Write the body

The body is a **profile** in the third person ("A marketing officer in Amman who orders lunch three times a week…"), under the headings the guide lists. Minerva builds the customer's prompt from it, so it describes the person and gives no orders to play them. Use real values: amounts, product names, places. Dialect, nationality, currency and city live here, never in a scenario. What happened on one call, and anything the customer hides on it, belong to the scenario. Lines starting with `>` are notes to authors.

## Check, then save

Before each save: the language and lexicon pair is in the guide's list, the body reads as a profile, and nothing in it is specific to one call.

- New: `personas_save` with no `id` and a fresh `idempotencyKey`.
- Edit: `personas_get`, change, then `personas_save` with the same `id` and the **full** content, `advanced` included (leaving it out drops the advanced settings).
- Then re-save every preset that pins this persona, so drills use the new version (`building-presets`).
