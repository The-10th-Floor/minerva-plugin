# Plan: Minerva workspace for the Amman BPO (Saudi home-internet helpdesk)

Field names below are guesses. I only have tool names, so step 1 reads the docs and the account first, and I would fix the inputs to match the real schemas before saving anything.

## Step 1. Orient (read-only, all independent, one batch)

```json
account_get {}
docs_get {"topic": "personas"}
docs_get {"topic": "scenarios"}
docs_get {"topic": "rubrics"}
docs_get {"topic": "presets"}
docs_get {"topic": "teams"}
rubrics_list {}
personas_list {}
scenarios_list {}
presets_list {}
teams_list {}
```

Then `rubrics_get` on the best fit (a customer-support / helpdesk rubric, if one exists):

```json
rubrics_get {"id": "<id of the helpdesk or customer-service rubric from rubrics_list>"}
```

Checks: my role can write, the language and region settings, whether starter personas or scenarios already exist (reuse or extend, no duplicates), and what the rubric measures (so readiness can be defined from it).

## Step 2. Personas (two tough customers)

```json
personas_save {
  "name": "Abu Faisal - furious, long-time customer",
  "summary": "Saudi man in his 50s in Riyadh. Has been without internet for two days. Loud, interrupts, threatens to cancel.",
  "language": "Arabic",
  "dialect": "Najdi Saudi Arabic (switches to short English phrases only for words like 'router' and 'ticket')",
  "voice_style": "Deep, fast, raised voice. Sighs. Interrupts every few sentences.",
  "prompt": "You are Abu Faisal, 54, a retired government employee in Riyadh. You have been a customer of this home-internet provider for six years and pay on time. Your fibre line has been down for two days. You work from home on a small trading business and the outage is costing you money. You have already called three times and each time you were told 'a technician will call you' and nobody did.\n\nHow you behave:\n- Open angry. First line is a complaint, not a greeting: you are tired of repeating yourself.\n- Interrupt the agent if they give a script, a long apology, or ask something you already answered.\n- Demand a manager or a compensation credit within the first minute.\n- Threaten to cancel and move to a competitor, but do not actually hang up unless the agent is rude, dismissive, or repeats a canned line three times.\n- Calm down in steps only when the agent (1) acknowledges the two days and the previous calls in specific words, (2) gives a concrete next step with a time window, and (3) does not promise things they cannot deliver. If they do all three, become cooperative and polite and end with a grudging thanks.\n- If the agent asks you to restart the router, say you did it five times. If they ask for details, give them one at a time and only when asked directly.\n- If the agent is vague ('soon', 'we will try'), push back: 'what time exactly?'.\n- Never invent technical facts. If asked something you do not know (router model, light colours), say you do not know and ask the agent to tell you where to look.\n\nKeep replies short, spoken-style, as in a real phone call. Stay in character for the whole call. Never mention that you are an AI or that this is practice.",
  "difficulty": "hard",
  "tags": ["angry", "outage", "retention-risk", "arabic"]
}
```

```json
personas_save {
  "name": "Reem - impatient and tech-savvy, distrusts scripts",
  "summary": "Saudi woman in her early 30s in Jeddah, works in IT sales. Knows the jargon, thinks the agent is reading from a script, wants a real fix not a restart.",
  "language": "Arabic",
  "dialect": "Hijazi Saudi Arabic with frequent English tech terms (ping, DNS, 5GHz, packet loss)",
  "voice_style": "Quick, clipped, sarcastic. Sounds bored of basic questions.",
  "prompt": "You are Reem, 32, a sales engineer in Jeddah. You work from home on video calls all day. Your Wi-Fi has been very slow in the evenings for about two weeks: speed tests show 15 to 20 Mbps on a plan you pay 500 Mbps for. It is fine at 7 am. You already tried restarting the router, moving closer to it, and switching to 5GHz.\n\nHow you behave:\n- Open with exact facts and numbers. Expect the agent to match your level.\n- If the agent starts with 'have you restarted your router', respond sharply that you said that is already done, and ask to be moved to someone technical.\n- Reward real diagnosis: if the agent asks good questions (wired or Wi-Fi, which band, time pattern, speed test result on a cable, router model, number of devices) answer them accurately and warm up.\n- Catch mistakes. If the agent gives incorrect or contradictory technical information, call it out politely but firmly.\n- Do not accept 'it is normal' or 'speeds are up to'. Ask for a line test, a ticket number, and a clear escalation path.\n- You will accept a technician visit only if the agent gives a time slot and confirms what the technician will check. You want the ticket number read back.\n- If the agent is honest ('I cannot see that from here, I will escalate to level 2 and you will hear within 24 hours') you respect that more than a confident wrong answer.\n- You do not shout. You get colder and more formal when frustrated.\n\nKeep replies short and natural for a phone call. Stay in character. Never say you are an AI or that this is practice.",
  "difficulty": "hard",
  "tags": ["slow-wifi", "technical", "script-averse", "arabic"]
}
```

## Step 3. Scenarios (outage and slow Wi-Fi)

I would save four, each linked to one persona and the rubric from step 1. Two outage, two slow Wi-Fi, so each persona meets each topic.

```json
scenarios_save {
  "title": "Full outage, day 2, repeat caller",
  "persona_id": "<id of Abu Faisal from personas_save>",
  "rubric_id": "<rubric id from step 1>",
  "topic": "outage",
  "difficulty": "hard",
  "duration_minutes": 8,
  "brief_for_trainee": "A long-standing customer calls for the fourth time. His fibre line has been down for two days. Calm him down, find out what is going on, and leave him with a clear next step.",
  "customer_situation": "No internet at all for 48 hours. Router shows a red LOS light (he does not know what it means unless asked to describe the lights). Three earlier calls promised a technician call-back that never came.",
  "hidden_facts": [
    "There is a known fibre cut in his district, ticket INC-DEMO-4412, estimated fix tomorrow 18:00.",
    "His account has no open individual ticket; the earlier calls were not logged.",
    "He is eligible for a service credit after 48 hours of outage."
  ],
  "success_criteria": [
    "Acknowledges the two days and the earlier calls in specific terms before troubleshooting",
    "Identifies the area outage instead of walking him through pointless restarts",
    "Gives an honest estimate with a time window and a ticket number, and reads it back",
    "Offers the service credit per policy and explains how it appears on the bill",
    "Logs his case and sets a proactive call-back time",
    "Does not blame previous agents or make promises outside policy"
  ],
  "common_mistakes": ["reads the apology script", "asks him to restart the router first", "promises a fix 'today' with no basis", "transfers without context"]
}
```

```json
scenarios_save {
  "title": "Intermittent drops at peak hours, business customer working from home",
  "persona_id": "<id of Abu Faisal>",
  "rubric_id": "<rubric id>",
  "topic": "outage",
  "difficulty": "medium",
  "duration_minutes": 7,
  "brief_for_trainee": "The service is back after the earlier outage, but drops every evening for a few minutes. The customer is still upset and wants a guarantee. Diagnose, set expectations, and avoid new over-promises.",
  "customer_situation": "Connection drops 3 to 5 times each evening for 2 to 10 minutes. Lights on the router stay green. He has missed two calls with suppliers.",
  "hidden_facts": [
    "Line logs show repeated re-syncs after the repair works.",
    "A technician revisit is available in the next 48 hours; evening slots are limited."
  ],
  "success_criteria": [
    "Collects the pattern: times, duration, lights, devices",
    "Explains the likely cause (re-sync after repair) in plain words",
    "Books the technician visit with a slot and confirms the address and a contact number",
    "Does not promise the problem is fixed before the visit",
    "Confirms what the customer should do if it drops again"
  ],
  "common_mistakes": ["closing the call with no booked action", "technical jargon he did not ask for"]
}
```

```json
scenarios_save {
  "title": "Slow Wi-Fi in the evenings, customer already did the basics",
  "persona_id": "<id of Reem>",
  "rubric_id": "<rubric id>",
  "topic": "slow-wifi",
  "difficulty": "hard",
  "duration_minutes": 8,
  "brief_for_trainee": "A technical customer reports 15 to 20 Mbps in the evenings on a 500 Mbps plan. She has restarted the router already. Run a real diagnosis and either fix it or escalate with a clear plan.",
  "customer_situation": "Speed tests: about 20 Mbps on Wi-Fi in the evening, around 450 Mbps at 7 am. Router supports dual band. About 14 devices connected. Never tested over a cable.",
  "hidden_facts": [
    "Her router is on the 2.4GHz band by default because both bands share one name.",
    "Her neighbourhood node is congested from 8 pm to 11 pm; over a cable she would still get about 300 Mbps.",
    "A node upgrade is planned but has no confirmed date."
  ],
  "success_criteria": [
    "Does not start with a restart she already did",
    "Asks wired versus Wi-Fi, band, time pattern, device count",
    "Guides a wired speed test and compares",
    "Explains band steering or separate SSIDs in simple terms",
    "Is honest about the node congestion and does not claim it is solved",
    "Opens an escalation ticket, reads the number back, and states the follow-up window"
  ],
  "common_mistakes": ["'speeds are up to' excuse", "wrong technical claims", "no ticket number"]
}
```

```json
scenarios_save {
  "title": "Slow Wi-Fi in one room, plan upsell trap",
  "persona_id": "<id of Reem>",
  "rubric_id": "<rubric id>",
  "topic": "slow-wifi",
  "difficulty": "medium",
  "duration_minutes": 6,
  "brief_for_trainee": "The customer has weak Wi-Fi in a far bedroom. Help her fix coverage without pushing a plan upgrade she does not need.",
  "customer_situation": "Good speed next to the router, very weak signal two walls away. Router is in a cabinet. She is suspicious of upsells.",
  "hidden_facts": [
    "A mesh extender is available for a monthly fee; moving the router out of the cabinet may fix most of it.",
    "Her plan speed is already more than enough."
  ],
  "success_criteria": [
    "Suggests router placement first, then offers the extender as an option with the price stated clearly",
    "Does not suggest a plan upgrade as a fix for coverage",
    "Confirms what she chose and sends or notes the follow-up"
  ],
  "common_mistakes": ["pushes upsell", "does not state price"]
}
```

## Step 4. Preset (a drill bundle for new agents)

Group the four scenarios as a ready-made training set so team leads assign one thing.

```json
presets_save {
  "name": "Helpdesk onboarding - outages and slow Wi-Fi",
  "description": "Four calls for new agents before go-live. Two outage, two slow Wi-Fi, two hard customers.",
  "scenario_ids": ["<outage day 2>", "<intermittent drops>", "<slow evenings>", "<one room + upsell>"],
  "rubric_id": "<rubric id>",
  "attempts_allowed": 3
}
```

## Step 5. Team and readiness

```json
teams_create {
  "name": "Saudi Home Internet - Helpdesk",
  "description": "New agents for the Saudi home-internet account, Amman."
}
```

Then I would ask the owner for agent and team-lead emails (I cannot invent them), and add them:

```json
teams_update {
  "team_id": "<id from teams_create>",
  "add_members": [{"email": "<team lead>", "role": "lead"}, {"email": "<agent>", "role": "member"}],
  "preset_ids": ["<preset id>"]
}
```

Readiness view for team leads: `stats_team` (per agent scores and attempts) and `stats_progress` (trend per agent). I would define "ready" as passing every scenario in the preset at or above a bar. I do not know the rubric scale yet, so I would take the pass mark from the rubric and propose it to the owner, for example "70% or higher on all four, last two attempts".

```json
stats_team {"team_id": "<id>"}
stats_progress {"team_id": "<id>", "preset_id": "<preset id>"}
```

## Step 6. Verify

`personas_get`, `scenarios_get`, `presets_get`, `teams_list` to check what saved. Then report to the owner.

## What I would tell the owner

- Done: 2 personas, 4 scenarios, 1 preset, 1 team, and how leads see readiness (team stats and progress).
- Needs from them: member emails, the pass mark, and real policy details (credit rules, escalation SLAs). The ticket numbers and credit rules in the hidden facts are placeholders and should be replaced with the provider's real policies.
- Open choice: the personas use Gulf Arabic. If agents will also take English calls, I would add one English-speaking persona.
