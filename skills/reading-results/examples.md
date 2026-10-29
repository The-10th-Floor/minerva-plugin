# Reading results: two worked examples

The values below are **illustrative**: invented for teaching, in the shape the tools return, trimmed to the fields being read. The rubric is the default "Customer call essentials" (criteria `c1` to `c10` in its order); the preset is the starter "Fibre outage × impatient power user".

## 1. One scorecard (`evaluations_get`)

```json
{
  "status": "scored",
  "evaluations": [{
    "rubric": { "id": "rub_essentials", "v": 1 },
    "result": {
      "total": 48.3, "passed": 1, "items": 3,
      "criteria": [
        { "type": "passFail", "criterionId": "c1", "passed": false,
          "comment": "No repair window or ticket number was given before the customer hung up.",
          "evidence": [{ "turn": 14, "startSec": 212.4, "quote": "I'll raise it with the team and someone will call you." }] },
        { "type": "scored", "criterionId": "c3", "score": 2,
          "comment": "Asked the customer to restart the router after he said he had done it twice; never asked about the lights.",
          "evidence": [{ "turn": 4, "startSec": 41.0, "quote": "Could you restart the router for me first?" }] },
        { "type": "scored", "criterionId": "c4", "score": 4,
          "comment": "Acknowledged the two lost workdays early and by name.",
          "evidence": [{ "turn": 2, "startSec": 12.8, "quote": "Two days without a connection when you work from home, I understand." }] },
        { "type": "passFail", "criterionId": "c9", "passed": false,
          "comment": "Ran the restart script against a customer who had already done it, a named pitfall.",
          "evidence": [{ "turn": 4, "startSec": 41.0, "quote": "Could you restart the router for me first?" }] }
      ]
    },
    "coaching": [
      "Before any step, ask what the customer already tried and skip it.",
      "Ask what the lights show, then check the area outage board.",
      "Close with a ticket number, a repair window and the credit for the lost days."
    ],
    "timeline": { "durationSec": 236, "talkRatio": 0.62, "deadAirSec": 19, "interruptions": { "rep": 1, "customer": 6 } }
  }]
}
```

How to read it:

- **48.3 with 1 of 3 passed.** The outcome and the pitfalls both failed; only "No promises outside policy" passed. Weights matter: "Reached the outcome" carries 5, so failing it costs more than a weak Opening. A scored criterion counts as its share of 5 (a 4 is 80%), a failed pass/fail as zero.
- **Read the evidence, not just the number.** The same moment, turn 4 at 0:41, sinks Discovery and Avoided the pitfalls: one habit, two criteria. That is the coaching topic.
- **Empathy 4 is real strength.** Say so; coaching that names what went well lands better.
- **The timeline agrees.** The customer interrupted six times and the trainee held 62% of the talk time: a trainee talking through a script while an expert pushes back.
- **No `override`**, so these are the judge's values. With one, the manager's values are final and the drill's `score.status` reads `overridden`.

Plain reading for a team lead: "Ahmad lost this call at 0:41 by asking for a restart the customer had already done twice. That one move cost Discovery and the pitfalls check. He opened with real empathy. Next: the same preset, asking what was tried before any step."

## 2. One person's progress (`stats_progress`)

```json
{
  "name": "Ahmad", "calls": 9, "callsThisWeek": 4,
  "streak": { "current": 3, "best": 5 },
  "average": { "value": 63.5, "calls": 8 },
  "rubrics": [{
    "name": "Customer call essentials", "calls": 8, "latest": 74.1, "best": 74.1, "mean": 63.5,
    "criteria": [
      { "title": "Reached the outcome", "type": "passFail", "latest": 1, "mean": 0.5 },
      { "title": "Discovery", "type": "scored", "latest": 4, "best": 4, "mean": 2.6 },
      { "title": "Empathy", "type": "scored", "latest": 4, "best": 5, "mean": 4.1 },
      { "title": "Avoided the pitfalls", "type": "passFail", "latest": 1, "mean": 0.38 }
    ]
  }]
}
```

How to read it:

- **9 calls, 8 scored.** One call is not in the average: it is pending, failed or system-ended. `average` has no `previous` yet because fewer than 20 calls are scored.
- **Totals and criteria use different scales.** Rubric totals are 0 to 100; a scored criterion is 1 to 5; a pass/fail `mean` is a pass rate. "Reached the outcome 0.5" means half his scored calls reached the outcome.
- **Weakest first.** Avoided the pitfalls (38%) and Discovery (2.6 of 5) are the coaching topics; Empathy (4.1) is a strength.
- **Latest beats mean on Discovery (4 against 2.6).** He is improving, but one call is not a trend. Read his last three drills with `evaluations_get` before calling it fixed.
- **Check what he ran.** Eight calls on the easiest preset and eight on the hardest are different stories: list his drills (`drills_list` with `repUid`) and group them by preset before judging readiness.

Plain reading: "Ahmad practices steadily (4 calls this week, a 3-day streak). His outcome rate is 50% and he avoids the pitfalls in only 38% of calls, mostly by repeating steps the customer already did. His last call was his best (74). Not ready yet: two more passes on the hardest outage preset would show it holds."
