---
name: reading-results
description: Use when interpreting Minerva drill results, scores, scorecards or statistics, explaining what a number means, comparing trainees or calls, or when a drill shows failed, pending or overridden.
---

# Reading results

`docs_get drills` and `docs_get stats` define every field. This skill is how to read them. A worked reading of a scorecard and of a progress report is in [examples.md](examples.md).

## Which calls count

A drill's `status` runs reserved, connecting, live, then `ended` or `failed`. Only calls that **ended after going live** count in calls, averages and streaks.

| `endReason` | Means | Counts and uses a credit |
| --- | --- | --- |
| `rep_hangup` | The trainee hung up | Yes |
| `customer_ended` | The AI customer ended it: satisfied, or gave up or escalated as the scenario says | Yes |
| `cap_reached` | The scenario's time cap ran out | Yes |
| `rep_disconnected` | The trainee's connection dropped | Yes, once live |
| `connection_failed`, `agent_dispatch_failed`, `provider_error`, `worker_crash` | A system failure | No: the credit is released |

`quality` is the trainee's own feedback: `simulation` low or `realistic` false points at the AI customer, not the trainee.

## Scores

- `score.status`: `pending` (the judge is working), `scored`, `failed` (run `evaluations_reevaluate`), `overridden` (a manager set their own values). `evaluations_reevaluate` takes `drillIds` (1–50) and also re-evaluates `scored` drills when the trainee disputes the score: the drill's rep, their managers or owners can run it, and the new score replaces the old one. Each drill keeps its rubrics, or pass `rubricIds` to use those at their current version; deleted rubrics are skipped and the org's default rubric stands in when none is left. It returns one result per drill: refused once `overridden`, and with `catalog_deleted` when the drill's scenario or persona was deleted.
- Per rubric, `total` is 0 to 100 from the weighted scored and pass/fail criteria; `passed` of `items` counts the pass/fail ones. A notes-only rubric has no number. A drill's score is the mean of its rubrics.
- `evaluations_get` gives, per rubric, the judge's `result` (each criterion's 1–5 `score` or `passed`, a `comment`, and `evidence` quotes with `turn` and `startSec`), three `coaching` tips, `timeline` metrics (talk ratio, words per minute, fillers, dead air, interruptions, response latency) and any `override`: the manager's values, note and up to three coaching actions. The final values, judge's or manager's, are in the drill's `score`.

## Statistics

- `stats_team`: `current` is the last 4 weeks, `previous` the 4 before. `performers` lists only trainees with 2 or more scored calls in the period. `trainees` covers the last 30 days; `toReview` counts scored calls no manager has reviewed. `weekly` is 8 weekly averages, `null` for a week with no scored call.
- `stats_progress`: `average` is the last 10 scored calls against the 10 before. Per rubric, `latest`, `best` and `mean` totals are 0 to 100. Per criterion, a scored one is 1 to 5, and a pass/fail one is 1 or 0, so its `mean` is a pass rate (0.6 means passed 6 calls in 10).

## Before you compare

Two numbers compare only when the calls match:

- **Same preset**, or the same persona and scenario: difficulty and the scenario's demands differ between pairs.
- **Same versions**: an edit makes a new version, and drills keep the version they ran (`evaluations_get` shows the rubric version as `rubric.v`).
- **Random controls**: a persona with `random` traits or mood rolls new values each drill, so one hard roll can sink one call. Read several.
- **Enough calls**: three or fewer is an anecdote. Say how many calls stand behind every average.
- **Counted calls only**: leave out failed and system-ended drills.
