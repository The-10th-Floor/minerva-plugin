---
name: querying-minerva
description: Use when looking something up in Minerva, such as a persona, scenario or preset by words, a trainee's or team's drills, calls in a date range, or numbers for a report, or when a Minerva list comes back partial or paged.
---

# Querying Minerva

Every read tool returns JSON you can count and quote. Pick the tool by the question, then read the result with `reading-results`.

## Which tool answers which question

| Question | Tool |
| --- | --- |
| Who am I, in which workspaces, with which role | `account_get` |
| Find a persona, scenario, rubric or preset by words | `search` (every workspace at once, 20 results, every word must match), then `fetch` for the full text |
| The whole library of one kind, or one item and its versions | `personas_list`, `scenarios_list`, `presets_list` (by `kind`), `rubrics_list`, then the matching `*_get` |
| Who is in which team, who has no team, their uids | `teams_list` |
| A team's activity, averages, best and weakest performers, calls to review | `stats_team` |
| One person's trend, streak, and per-criterion latest, best and average | `stats_progress` |
| Which calls were made, by whom, on which preset, when | `drills_list` |
| One call's status and score | `drills_get` |
| Why a call scored what it did | `evaluations_get` |

`search` covers the library only; drills and people come from the tools below it.

## Filters and pages

- `drills_list` filters by `repUid`, `teamId`, `presetId` and an ISO 8601 range (`from` inclusive, `to` exclusive). It returns 50 newest first and a `nextCursor`; pass it back as `cursor` until none comes back. With two filters at once a page can hold fewer than 50, so keep following the cursor rather than stopping at a short page.
- A manager's own drills are outside their teams' list: pass their own uid as `repUid`.
- `stats_progress` pages its drills 20 at a time with the same `nextCursor`; its aggregates repeat on every page, so read them once.
- `stats_team` takes an optional `teamId`; when `truncated` is true only the newest 1,000 drills were counted, so narrow to one team.
- Library lists return 50 per page with `nextCursor` too.
- Uids for `repUid` and `stats_progress` come from `teams_list`; team ids too.
- With several workspaces, pass `orgId` to every tool except `search` and `fetch`.
- Pass the person's `timeZone` ("Asia/Amman", "Asia/Riyadh") to `stats_progress`, or days and streaks follow UTC.

## Answer with the numbers behind them

Every figure you report names its source and window: "4 scored calls on Fibre outage × impatient power user since 2026-10-01 (drills_list), average 71". A count you could not finish (a page you did not follow, `truncated`) is reported as partial.
