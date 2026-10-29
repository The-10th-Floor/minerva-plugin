---
name: coaching-from-drills
description: Use when reviewing Minerva drills or scores, deciding who on a team is ready for live calls, finding a trainee's weak spots, or writing coaching after a practice call.
---

# Coaching from drills

Agents read drills and their scores; trainees start drills in the app. Find the data with `querying-minerva` and read every number with `reading-results` (what counts, the scales, and when two numbers compare).

## The team view

`stats_team`, then start a review session from each trainee's `toReview`.

## One person

1. `stats_progress` with their `uid` (from `teams_list`) and their `timeZone` ("Asia/Amman", "Asia/Riyadh"). The criteria with the lowest averages are the coaching topic.
2. `drills_list` filtered to them, then `evaluations_get` on a recent drill for the judge's comment and quoted evidence.
3. Coach from the evidence: quote the moment, name what to do instead, and pick the next preset that practices it (`building-presets`).

## Readiness

Readiness is judged against a bar the person agreed: for example, every preset in the call type's ladder passed at or above an agreed score, with the top rung run at least twice. With no agreed bar yet, propose one, mark every verdict **provisional** against it, and ask the person to confirm it before anyone moves to live calls. Report each trainee against the bar with the drills behind it; a trainee with too few counted calls on a rung is "not enough data", whatever the average.

## Change a score

`evaluations_override` sets the manager's own values, notes and up to three coaching actions, and the trainee sees them. Show the person the change and get their yes before sending `confirm: true`. `evaluations_reevaluate` (`drillIds`) re-runs the judge on failed or disputed drills.
