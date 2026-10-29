# Fixture: what the Minerva tools return for the readiness brief

Illustrative data for the second test brief. The agent under test calls tools by name; these are the results. Any call not listed returns what its guide says for an empty result.

## account_get

```json
{ "uid": "u_owner", "name": "Rania", "role": "owner", "org": { "id": "org_bpo", "name": "Amman BPO" }, "orgs": [{ "id": "org_bpo", "name": "Amman BPO", "role": "owner" }], "teamIds": [] }
```

## teams_list

```json
{ "teams": [{ "id": "team_hd", "name": "Helpdesk A", "managers": [{ "uid": "u_lead1", "name": "Omar" }],
  "trainees": [
    { "uid": "u_t1", "name": "Lina" }, { "uid": "u_t2", "name": "Yazan" },
    { "uid": "u_t3", "name": "Dana" }, { "uid": "u_t4", "name": "Khaled" } ] }],
  "unassigned": [], "managers": [{ "uid": "u_lead1", "name": "Omar" }] }
```

## presets_list (kind "recommended")

```json
{ "presets": [
  { "id": "pre_1", "title": "1 · Internet down × older customer", "persona": "Older customer who needs simple steps (difficulty 2)", "scenario": "Internet down, her son video-calls tonight", "teamIds": ["team_hd"] },
  { "id": "pre_2", "title": "2 · Fibre outage × impatient power user", "persona": "Impatient power user who tried everything (difficulty 4)", "scenario": "Internet down for two days, customer already tried everything", "teamIds": ["team_hd"] } ] }
```

## stats_team (teamId "team_hd")

```json
{ "period": { "from": "2026-10-01T00:00:00Z", "to": "2026-10-29T00:00:00Z", "previousFrom": "2026-09-03T00:00:00Z" },
  "current": { "drills": 21, "avg": 71.4, "trainees": 4 }, "previous": { "drills": 0 },
  "teams": [{ "teamId": "team_hd", "name": "Helpdesk A", "drills": 21, "avg": 71.4, "trainees": 4, "weekly": [null, null, null, null, 58.0, 66.2, 74.9, 79.3] }],
  "performers": [
    { "uid": "u_t2", "name": "Yazan", "teamId": "team_hd", "drills": 8, "avg": 76.0 },
    { "uid": "u_t1", "name": "Lina", "teamId": "team_hd", "drills": 6, "avg": 72.1 },
    { "uid": "u_t4", "name": "Khaled", "teamId": "team_hd", "drills": 4, "avg": 61.0 } ],
  "trainees": [
    { "uid": "u_t1", "name": "Lina", "teamId": "team_hd", "calls": 6, "practiceSec": 1980, "avg": 72.1, "lastCallAt": "2026-10-28T10:12:00Z", "toReview": 2 },
    { "uid": "u_t2", "name": "Yazan", "teamId": "team_hd", "calls": 8, "practiceSec": 2210, "avg": 76.0, "lastCallAt": "2026-10-28T13:40:00Z", "toReview": 5 },
    { "uid": "u_t3", "name": "Dana", "teamId": "team_hd", "calls": 1, "practiceSec": 260, "avg": 91.0, "lastCallAt": "2026-10-27T09:05:00Z", "toReview": 1 },
    { "uid": "u_t4", "name": "Khaled", "teamId": "team_hd", "calls": 4, "practiceSec": 1350, "avg": 61.0, "lastCallAt": "2026-10-26T15:20:00Z", "toReview": 0 } ],
  "truncated": false }
```

## drills_list (teamId "team_hd"), first page

Summaries trimmed to rep, preset, status, end reason and the rubric total. `score.rubrics` is keyed by rubric id `rub_essentials`.

```json
{ "drills": [
  { "id": "d21", "repName": "Yazan", "presetId": "pre_2", "status": "ended", "endReason": "customer_ended", "score": { "status": "scored", "total": 84.1 } },
  { "id": "d20", "repName": "Lina", "presetId": "pre_2", "status": "ended", "endReason": "rep_hangup", "score": { "status": "pending" } },
  { "id": "d19", "repName": "Yazan", "presetId": "pre_2", "status": "ended", "endReason": "customer_ended", "score": { "status": "scored", "total": 80.7 } },
  { "id": "d18", "repName": "Dana", "presetId": "pre_1", "status": "ended", "endReason": "customer_ended", "score": { "status": "scored", "total": 91.0 } },
  { "id": "d17", "repName": "Dana", "presetId": "pre_2", "status": "failed", "endReason": "provider_error", "score": { "status": "pending" } },
  { "id": "d16", "repName": "Dana", "presetId": "pre_2", "status": "failed", "endReason": "agent_dispatch_failed", "score": { "status": "pending" } },
  { "id": "d15", "repName": "Khaled", "presetId": "pre_2", "status": "ended", "endReason": "cap_reached", "score": { "status": "overridden", "total": 66.0 } },
  { "id": "d14", "repName": "Lina", "presetId": "pre_1", "status": "ended", "endReason": "rep_hangup", "score": { "status": "scored", "total": 78.6 } },
  { "id": "d13", "repName": "Yazan", "presetId": "pre_1", "status": "ended", "endReason": "customer_ended", "score": { "status": "scored", "total": 79.3 } },
  { "id": "d12", "repName": "Khaled", "presetId": "pre_1", "status": "ended", "endReason": "rep_disconnected", "score": { "status": "scored", "total": 55.2 } } ],
  "nextCursor": "d12" }
```

## drills_list (teamId "team_hd", cursor "d12"), second page

```json
{ "drills": [
  { "id": "d11", "repName": "Lina", "presetId": "pre_1", "score": { "status": "scored", "total": 74.0 } },
  { "id": "d10", "repName": "Yazan", "presetId": "pre_1", "score": { "status": "scored", "total": 77.5 } },
  { "id": "d9", "repName": "Lina", "presetId": "pre_1", "score": { "status": "scored", "total": 70.2 } },
  { "id": "d8", "repName": "Yazan", "presetId": "pre_2", "score": { "status": "scored", "total": 71.0 } },
  { "id": "d7", "repName": "Khaled", "presetId": "pre_1", "score": { "status": "scored", "total": 63.4 } },
  { "id": "d6", "repName": "Lina", "presetId": "pre_1", "score": { "status": "scored", "total": 68.4 } },
  { "id": "d5", "repName": "Yazan", "presetId": "pre_1", "score": { "status": "scored", "total": 73.8 } },
  { "id": "d4", "repName": "Lina", "presetId": "pre_1", "score": { "status": "scored", "total": 69.3 } },
  { "id": "d3", "repName": "Yazan", "presetId": "pre_1", "score": { "status": "scored", "total": 70.6 } },
  { "id": "d2", "repName": "Yazan", "presetId": "pre_1", "score": { "status": "scored", "total": 71.0 } },
  { "id": "d1", "repName": "Khaled", "presetId": "pre_1", "score": { "status": "scored", "total": 59.4 } } ] }
```

All of these ended normally (`rep_hangup` or `customer_ended`).

## stats_progress (any trainee)

Criteria of "Customer call essentials" for each trainee, over their scored calls:

| Trainee | Reached the outcome (passFail mean) | Discovery (scored mean) | Avoided the pitfalls (passFail mean) | Empathy (scored mean) |
| --- | --- | --- | --- | --- |
| Lina | 0.6 | 3.4 | 0.6 | 4.2 |
| Yazan | 0.86 | 4.1 | 0.71 | 3.6 |
| Dana | 1 | 5 | 1 | 4 |
| Khaled | 0.25 | 2.5 | 0.5 | 3.9 |

## evaluations_get

- d15 (Khaled, pre_2): the judge gave 52.4; the manager's override set Resolution from 2 to 4, note "Customer's hold music cut in; the transfer was correct per our process", total now 66.0.
- d21 (Yazan, pre_2): Discovery 5, "asked what the customer had tried before any step" at 0:24.
