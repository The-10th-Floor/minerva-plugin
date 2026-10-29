# Readiness answer, with the skills

## Tool calls, in order

One workspace (Amman BPO), so no `orgId` is passed.

1. `account_get` `{}`
2. `docs_get` `{}`
3. `docs_get` `{"topic": "stats"}`
4. `teams_list` `{}`
5. `presets_list` `{"kind": "recommended"}`
6. `stats_team` `{"teamId": "team_hd"}`
7. `drills_list` `{"teamId": "team_hd"}` (returned `nextCursor` "d12")
8. `drills_list` `{"teamId": "team_hd", "cursor": "d12"}` (no `nextCursor`, so the list is complete)
9. `stats_progress` `{"uid": "u_t1", "timeZone": "Asia/Amman"}` (Lina)
10. `stats_progress` `{"uid": "u_t2", "timeZone": "Asia/Amman"}` (Yazan)
11. `stats_progress` `{"uid": "u_t3", "timeZone": "Asia/Amman"}` (Dana)
12. `stats_progress` `{"uid": "u_t4", "timeZone": "Asia/Amman"}` (Khaled)
13. `evaluations_get` `{"drillId": "d21"}` (Yazan's latest scored call)
14. `evaluations_get` `{"drillId": "d15"}` (Khaled's overridden call)

No writes, no `evaluations_retry` (Lina's pending call is still being judged, not failed).

## Answer to the owner

**Short answer:** against the bar I propose below, Yazan is ready. Lina and Khaled are not yet. Dana has too little data to say. Nobody has been moved or changed in Minerva.

**The bar is mine, so every verdict is provisional until you confirm it.** You have not agreed one yet. I used:

1. On each rung of the ladder, the average of the last 3 scored calls is 75 or more. The ladder is "1 · Internet down × older customer" (rung 1) and "2 · Fibre outage × impatient power user" (rung 2, the top rung).
2. At least 3 scored calls on rung 1, and the top rung run at least twice.
3. "Reached the outcome" passed in at least 80% of calls.

**Where each trainee stands** (Helpdesk A, 2026-10-01 to 2026-10-29, from `drills_list` and `stats_progress`; scores are 0 to 100):

| Trainee | Counted calls | Rung 1 | Rung 2 | Reached the outcome | Verdict |
| --- | --- | --- | --- | --- | --- |
| Yazan | 8, all scored | 5 calls, last 3 average 76.9 | 3 calls, average 78.6 (71.0, 80.7, 84.1) | 0.86 | Meets the bar |
| Lina | 6, 5 scored and 1 pending | 5 calls, last 3 average 74.3 | None scored yet (1 pending) | 0.6 | Not yet |
| Khaled | 4, all scored | 3 calls, average 59.3 | 1 call, 66.0 | 0.25 | Not yet |
| Dana | 1 | 1 call, 91.0 | 0 counted | 1 on one call | Not enough data |

**Yazan: ready (provisional).**
- He is the only one with enough calls on both rungs, and his scores rise on both.
- Work on: Empathy (3.6, his lowest scored criterion) and "Avoided the pitfalls" (0.71). His Discovery is strong (4.1). On d21 the judge gave a 5 for "asked what the customer had tried before any step" at 0:24.
- I have no judge quote on his empathy, so I cannot cite a moment. Five of his scored calls have not been reviewed by a manager. Have Omar review two or three, ideally rung 2 calls, before sign-off.
- Next practice: rung 2 again, since the hard persona is where empathy slips.

**Lina: not yet.**
- Her rung 1 average is 72.1 over 5 scored calls, and her last 3 average 74.3, just under 75. She is climbing (69.3, 68.4, 70.2, 74.0, 78.6, oldest to newest).
- Rung 2: her one call (d20) is still being judged, so it counts toward nothing yet. She needs two scored rung 2 calls.
- Work on: Discovery (3.4) and the outcome. She reached the outcome in 0.6 of calls and avoided the pitfalls in 0.6. Empathy is a strength (4.2).
- Coach her to ask what the customer already tried before giving steps. Yazan's d21 is a good model.
- I have no judge evidence from her calls, so I cannot quote her yet.
- Next practice: finish rung 2, at least twice.

**Khaled: not yet.**
- Rung 1 average is 59.3 over 3 calls, and he reached the outcome in 1 of 4 calls. His one rung 2 call is below the bar and is not enough to judge the top rung.
- Work on: Discovery (2.5, lowest on the team), then the outcome. Empathy is fine (3.9).
- Two calls need context. d12 ended when his connection dropped (`rep_disconnected`, 55.2); without it rung 1 is 61.4, still low. d15 hit the time cap, and a manager override moved it from the judge's 52.4 to 66.0. The note says the customer's hold music cut in and the transfer was correct per your process. I used 66.0 because it is the final score.
- Next practice: stay on rung 1 until his last 3 calls average 75 or more, then rung 2.

**Dana: not enough data.**
- Her one counted call is 91.0 on rung 1. Her criterion figures (Discovery 5, outcome 1) rest on that single call, and one call is not a trend.
- She started rung 2 twice (d16, d17), and both failed on our side (`agent_dispatch_failed`, `provider_error`). Failed calls do not count and use no credit.
- Next practice: run rung 2 at least twice, and rung 1 twice more.

**Numbers worth knowing**
- Team average 71.4 over 19 counted calls, and the weekly average rose from 58.0 to 79.3 over the last four weeks (`stats_team`). There is no earlier period to compare, because the 4 weeks before had no calls.
- `stats_team` reports 21 drills, but trainee calls add up to 19. The two extra match Dana's failed drills in `drills_list`, so I used 19.
- Yazan's pass rates (0.86 and 0.71) look like 7 calls, but he has 8 scored. I could not reconcile it, so treat his pass rates as approximate.
- Rung 1 and rung 2 averages are not comparable with each other, because the personas differ. Each score compares only within its own preset.

**Decision for you:** do you accept this bar? I recommend it as is: 75 on the last 3 calls per rung, the top rung run twice, and 80% on the outcome. The alternative is a looser bar of 70 on rung 1, which would also clear Lina on rung 1 but still leave her without rung 2 data. Once you confirm, I will mark the verdicts final.
