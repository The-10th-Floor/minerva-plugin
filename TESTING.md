# Testing the skills

Each skill is tested like code, following the writing-skills method: run a real brief with an agent that does not have the skills (RED), write down what goes wrong, then run the same brief with a fresh agent that has them (GREEN), fix the skills, and run again until the failures are gone.

All runs on 2026-10-29 used fresh Claude Sonnet subagents with no live tools: each wrote out the tool calls it would make and its answer. Where a run calls `docs_get`, it got the real guide text from `apps/web/lib/registry/guides.ts` with the values the server appends (the three dialect pairs, moods, call length, and the two worked examples), as if fetched.

## Brief 1: set up a workspace

> "We're a BPO in Amman taking over the helpdesk for a Saudi home-internet provider next month. Set up our workspace so new agents can practice: a couple of tough customers, calls about outages and slow Wi-Fi, and a way for team leads to see who's ready."

Setup given to the agent: owner of one workspace, empty library, the default rubric only, two possible leads and eight trainees in no team.

- RED: [testing/baseline-without-skills.md](testing/baseline-without-skills.md), with tool names only and no guides.
- GREEN: [testing/with-skills.md](testing/with-skills.md), the final run with every skill.

| Failure in RED | Fixed by | GREEN |
| --- | --- | --- |
| Invented dialects the platform does not serve (Najdi, Hijazi) | `writing-personas` § Pick the dialect: only listed pairs, mapped by caller country | Every persona is `ar` / `gulf`; the owner is told Minerva has one Gulf dialect and the city lives in the profile |
| Personas written as "You are…" role-play prompts | `writing-personas` § Write the body: a third-person profile Minerva builds the prompt from | Three third-person profiles under the guide's headings |
| Scenarios tied to personas (`persona_id` in the scenario) | `writing-scenarios` § Neutral and unpaired; `setting-up-a-workspace` grid | Scenarios carry no persona, dialect, nationality, currency or city; pairs are chosen in presets |
| Hidden facts with no revealing question | `writing-scenarios` § What makes a scenario work, and the check before saving | Every fact ends with its question; hidden truths are the customer's own; the area fault sits in `expectations` |
| A `docs_get` topic that does not exist (`teams`) | `getting-started` lists the exact topics | Only `overview`, `personas`, `scenarios`, `rubrics`, `presets`, `stats`, `drills` |
| The two helpdesk starters missed | `setting-up-a-workspace` step 1.2: match the brief to the starter sets, ask for a missing set to be added in the app | Names the technical support set, asks the owner to add it first, and uses its "Internet down, her son video-calls tonight" call as rung 1 |

Fixed between runs. The first GREEN run (same brief, before the fixes) passed the six failures above but wrote new scenarios instead of asking for the starter set, and saved everything on assumed defaults before the owner agreed. `setting-up-a-workspace` now says a missing starter set is added in the app first, and that "the first save waits for the person's yes to the plan". The final run does both.

Still open:

- Gender: a starter scenario can assume one ("her son"). The run paired it with a woman persona, and `setting-up-a-workspace` now says to check any gender the text assumes.
- This is a written plan, not a live run: tool inputs are checked by reading, not by the server's validation.

## Brief 2: who is ready

> "Which of my helpdesk trainees are ready for live calls, and what should each work on?"

The tool results come from [testing/fixtures/readiness-data.md](testing/fixtures/readiness-data.md): four trainees on a two-rung ladder, with traps (a trainee with one counted call and two system-failed calls, a pending score, an overridden score, a call that hit the time cap, a dropped connection, and a second page of drills behind `nextCursor`). Both runs had the `docs_get` guides, so the difference is the skills alone.

- RED: [testing/baseline-readiness-without-skills.md](testing/baseline-readiness-without-skills.md)
- GREEN: [testing/readiness-with-skills.md](testing/readiness-with-skills.md), the final run

The guides alone carried a lot: RED followed the cursor, left the system-failed calls out, and read pass/fail means as pass rates. What it got wrong, and what the skills changed:

| Failure in RED | Fixed by | GREEN |
| --- | --- | --- |
| Set its own readiness bar and cleared a trainee as a final verdict | `coaching-from-drills` § Readiness: propose a bar, mark verdicts provisional, ask the owner to confirm | "The bar is mine, so every verdict is provisional until you confirm it", with one decision for the owner |
| Led with a score trend that mixed the easy and hard presets | `reading-results` § Before you compare: same preset only | Separate columns per rung; notes the two rungs do not compare |
| Figures with no source or window | `querying-minerva` § Answer with the numbers behind them | Names the tools and the window (2026-10-01 to 2026-10-29) behind the table |
| Did not question the team totals | `reading-results` § Which calls count | Saw that `stats_team` counted 21 drills where trainee calls add up to 19 |
| Said nothing about credits for the failed calls | `reading-results` end-reason table | "Failed calls do not count and use no credit" |

Fixed between runs. The first GREEN run still proposed a bar and judged against it in the same breath. `coaching-from-drills` now says to mark verdicts provisional until the owner confirms the bar, and the final run does.

Still open:

- Two numbers in the fixture do not add up: `stats_team` counts the two failed drills in its 21, and Yazan's pass rates (0.86, 0.71) imply 7 scored calls, not 8. Both are fixture mistakes. The GREEN run flagged both instead of hiding them; the RED run noticed neither. The fixture is kept as run, so the two runs stay comparable.

## Running a test again

1. Give a fresh agent the brief, the tool names, the guide text, and (for GREEN) the skill paths. For brief 2, also the fixture.
2. Compare its output with the failure tables above.
3. When a skill changes, rerun both briefs, and add a row here for any new failure and its fix.
