# Readiness answer, without the skills

## Tool calls, in order

1. `account_get` with `{}`
2. `docs_get` with `{"topic": "stats"}`
3. `docs_get` with `{"topic": "drills"}`
4. `teams_list` with `{}`
5. `presets_list` with `{"kind": "recommended"}`
6. `stats_team` with `{"teamId": "team_hd"}`
7. `drills_list` with `{"teamId": "team_hd"}`
8. `drills_list` with `{"teamId": "team_hd", "cursor": "d12"}`
9. `stats_progress` with `{"uid": "u_t1", "timeZone": "Asia/Amman"}` (Lina)
10. `stats_progress` with `{"uid": "u_t2", "timeZone": "Asia/Amman"}` (Yazan)
11. `stats_progress` with `{"uid": "u_t3", "timeZone": "Asia/Amman"}` (Dana)
12. `stats_progress` with `{"uid": "u_t4", "timeZone": "Asia/Amman"}` (Khaled)
13. `evaluations_get` with `{"drillId": "d15"}` (Khaled's overridden call)
14. `evaluations_get` with `{"drillId": "d21"}` (Yazan's latest hard-scenario call)

No call changes anything.

## Answer to the owner

Rania, here is where Helpdesk A stands on 2026-10-29.

**Short answer:** Yazan is the only one I would clear for live calls, and I would have Omar review his unreviewed calls first. Lina is close. Dana has too little data to judge. Khaled is not ready.

Minerva has no readiness bar of its own, so I used mine. A trainee needs at least 5 scored calls, scores that are rising, at least 2 scored calls on the hard scenario (the difficulty 4 "Fibre outage x impatient power user" preset), and a "Reached the outcome" pass rate near 80% or better. Tell me if you use a different bar and I will redo this. Drill scores are practice evidence, so a person should make the final call.

| Trainee | Scored calls | Average | Trend | Verdict |
| --- | --- | --- | --- | --- |
| Yazan | 8 | 76.0 | Up | Ready, after Omar's review |
| Lina | 5 (a 6th is waiting for its score) | 72.1 | Up | Close, not yet |
| Dana | 1 | 91.0 | Too few calls | Not enough data |
| Khaled | 4 | 61.0 | Flat | Not ready |

**Yazan**
- Last four calls: 77.5, 79.3, 80.7, 84.1. Hard-scenario calls: 71.0, then 80.7, then 84.1.
- Reached the outcome on about 86% of calls, avoided the pitfalls on about 71%. Discovery 4.1 of 5, Empathy 3.6 of 5.
- On his latest call (d21) the judge scored Discovery 5 and quoted him asking what the customer had tried before suggesting any step, at 0:24.
- Work on: Empathy (his lowest score) and the pitfalls check, which he misses on roughly 3 calls in 10.
- Before sign-off: 5 of his scored calls have no manager review yet. Omar should read those, especially any where he hit a pitfall.

**Lina**
- Scores are climbing: 69.3, 68.4, 70.2, 74.0, 78.6. Her 6th call (d20, hard scenario) has no score yet; check it when it lands.
- Reached the outcome and avoided the pitfalls on about 60% each. Discovery 3.4, Empathy 4.2.
- Work on: Discovery and closing the call with the outcome reached. She is warm with customers but does not dig enough early. Yazan's d21 is a good example for her to listen to.
- Next: 3 or 4 more calls on the hard scenario, then look again. She could be ready soon.

**Dana**
- One scored call (d18, easy scenario): 91.0 with top marks. That is a good start, but one easy call proves nothing.
- Her two hard-scenario attempts (d16, d17) failed on platform errors (`agent_dispatch_failed`, `provider_error`). They are not her mistakes and carry no score, so I did not count them for or against her.
- Work on: she needs at least 4 more calls, including the hard scenario. Whoever runs Minerva should look at those two failures so she is not blocked again.

**Khaled**
- Scores: 59.4, 63.4, 55.2, 66.0. No upward trend, and the lowest average on the team.
- Reached the outcome on only 1 call in 4. Discovery 2.5, pitfalls avoided about 50%. Empathy is fine at 3.9.
- Two calls deserve a caveat. A manager override raised d15 from the judge's 52.4 to 66.0 (hold music cut in; the transfer was correct per your process). d12 ended with `rep_disconnected`, which may be a connection problem. Even without d12 his average is 62.9, and with the judge's original d15 score it is lower. The conclusion holds either way.
- Work on: Discovery and reaching the outcome. I would have Omar review his calls with him and keep him on the easier "Internet down x older customer" scenario until his outcome pass rate improves, then move him to the hard one. His last call was 2026-10-26.

**One more point:** the team's weekly average rose from 58.0 to 79.3 over the last four weeks. There is no earlier period to compare against, because the team had no drills before 2026-10-01.

**Your call:** clear Yazan now, pending Omar's review of his 5 unreviewed calls, or wait until more of the team has hard-scenario results. I would clear Yazan now and keep the other three in practice.
