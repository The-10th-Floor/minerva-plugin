# Plan: Minerva workspace for the Amman BPO (Saudi home-internet helpdesk), with the skills

Skills used: `getting-started`, `setting-up-a-workspace`, `writing-personas`, `writing-scenarios`, `choosing-rubrics`, `building-presets`, `coaching-from-drills`, `querying-minerva`, `reading-results`. Guides read through `docs_get` (overview, personas, scenarios, rubrics, presets, stats) take priority over the skills where they differ.

What I know from `account_get` and the lists: you are the owner of one workspace, "Amman BPO". The library is empty, so no starters were picked at sign-up. The only rubric is "Customer call essentials" (`rub_essentials`). There are no teams, two members who can manage a team (`u_lead1`, `u_lead2`) and eight trainees with no team (`u_t1` to `u_t8`).

---

## 1. What I send the owner first

**Message to the owner (nothing is saved until you say yes):**

> I read your brief and your workspace. It is empty, so I will build a small practice grid for the new helpdesk and give each team lead a view of who is ready. Here is the plan.
>
> **What you get**
>
> | Call type | Calls (scenarios) | Customers (personas) | Ladder, easy to hard |
> | --- | --- | --- | --- |
> | Outages | "Internet down, her son video-calls tonight" (Minerva starter), "Internet down since last night, red light on the fiber box" (new), "Third outage this month, wants a firm date and compensation" (new) | Patient non-technical mother (difficulty 2), impatient online-shop owner (4), distrustful customer who has heard it all before (5) | Outage 1: starter call with the mother. Outage 2: red-light call with the shop owner. Outage 3: third-outage call with the distrustful customer. |
> | Slow Wi-Fi | "Wi-Fi slow in the evenings, fast next to the router" (new) | Same three customers | Wi-Fi 1: the mother. Wi-Fi 2: the shop owner. |
>
> - **Two tough customers, one easy one.** The shop owner (4) and the distrustful customer (5) are the tough ones you asked for. The mother (2) is the first rung, so a new agent does not start at the hardest call.
> - **Saudi callers speak Gulf Arabic.** Minerva has Jordanian, Gulf and US English only, and Gulf is the nearest pair for Saudi Arabia. Your Amman agents will hear Gulf Arabic, which is the point. Minerva has no Najdi or Hijazi setting, so the city flavor (Riyadh, Jeddah, Dammam) is in each customer's profile and the dialect is the general Gulf one.
> - **Scoring.** Every call is judged on "Customer call essentials" (reached the outcome, avoided pitfalls, no promises outside policy, opening, discovery, empathy, resolution, objection handling, close, tone). It fits all four calls. If the client has its own QA form, send it and I will map it line by line for you to build in the app.
> - **Teams.** Two teams, each with one lead. I assume Helpdesk team 1 = lead `u_lead1` with trainees `u_t1` to `u_t4`, and Helpdesk team 2 = lead `u_lead2` with trainees `u_t5` to `u_t8`. Tell me if you want a different split. Both teams get all five recommended drills.
> - **Ready for live calls (proposed bar, provisional until you confirm).** A trainee is ready when the latest counted call on every drill in both ladders scored 70 or higher, and the top rung of each ladder (Outage 3 and Wi-Fi 2) scored 70 or higher on two counted calls. Fewer counted calls than that is "not enough data", whatever the average. Is 70 the right number for this client?
>
> **One thing you do first, in the app:** Library, New, from a template, and add the **Technical support** starter set. I use one of its calls (and its first rung) and the set is the base for the grid. Tell me when it is in. Its three default drills will also show for everyone: they use US English and Jordanian customers, so I will point the leads to the five Saudi drills instead.
>
> **Facts I do not have, so I wrote around them:** the client's name, its outage-credit rule, how fast it books a technician, and which tool shows area outages. The calls check behavior (looked for the outage, gave a dated visit, no invented credit) and not those numbers. Send them and I will tighten the calls and re-pin the drills.
>
> **One decision:** Build this client's practice in the "Amman BPO" workspace now (my pick), or first create a separate workspace for this client in the app, so its library, scores and access stay apart from your other clients? Pick the second only if you will serve other clients too.
>
> Say "yes" to the plan, and tell me when the starter set is added.

**Assumptions I carry if the owner only says "yes":** the team split above, bar of 70, the build stays in "Amman BPO", all calls in Arabic.

Totals: 3 personas, 3 scenarios, 5 presets, 2 teams. If a save returns `library_limit`, I stop, keep what is saved and tell the owner which rows are missing. I build the rows in the order that matters most (see section 2).

---

## 2. Tool calls after the owner says yes (and has added the starter set)

All calls use the single workspace, so no `orgId`. Ids written as `$NAME` are copied from the result of an earlier call and never typed from memory. No call here needs `confirm: true` (nothing is deleted, restored or overridden). Each change has its own fresh `idempotencyKey`.

### Step A. Read before writing

Run together:

```json
{"tool": "account_get", "input": {}}
```
```json
{"tool": "docs_get", "input": {"topic": "overview"}}
```
```json
{"tool": "docs_get", "input": {"topic": "personas"}}
```
```json
{"tool": "docs_get", "input": {"topic": "scenarios"}}
```
```json
{"tool": "docs_get", "input": {"topic": "rubrics"}}
```
```json
{"tool": "docs_get", "input": {"topic": "presets"}}
```
```json
{"tool": "teams_list", "input": {}}
```
```json
{"tool": "personas_list", "input": {}}
```
```json
{"tool": "scenarios_list", "input": {}}
```
```json
{"tool": "presets_list", "input": {"kind": "default"}}
```
```json
{"tool": "rubrics_list", "input": {}}
```
```json
{"tool": "rubrics_get", "input": {"id": "rub_essentials"}}
```

What I check in the results: the Technical support set is now in the library (`templateId` on its items); `rub_essentials` is the rubric to use; the dialect pairs listed for personas include `ar` / `gulf`; the call cap allows 60 to 600 seconds. From `scenarios_list` I take `$S_SON`, the id of the starter call "Internet down, her son video-calls tonight" (its title may be in Arabic). Then:

```json
{"tool": "scenarios_get", "input": {"id": "$S_SON"}}
```

I read it for anything that does not fit a Gulf Arabic woman in her fifties (a gender, a city, a currency). It was written neutral and says "her son", which fits the mother persona. If the text clashes, I leave that starter out, make Outage 1 the red-light call with the mother, and tell the owner.

### Step B. Teams

```json
{"tool": "teams_create", "input": {"name": "Helpdesk team 1", "managerUids": ["u_lead1"], "idempotencyKey": "ambpo-2026-10-29-team-1-create"}}
```
```json
{"tool": "teams_create", "input": {"name": "Helpdesk team 2", "managerUids": ["u_lead2"], "idempotencyKey": "ambpo-2026-10-29-team-2-create"}}
```

Then, with `$TEAM1` and `$TEAM2` from the results:

```json
{"tool": "teams_update", "input": {"teamId": "$TEAM1", "name": "Helpdesk team 1", "managerUids": ["u_lead1"], "traineeUids": ["u_t1", "u_t2", "u_t3", "u_t4"], "idempotencyKey": "ambpo-2026-10-29-team-1-trainees"}}
```
```json
{"tool": "teams_update", "input": {"teamId": "$TEAM2", "name": "Helpdesk team 2", "managerUids": ["u_lead2"], "traineeUids": ["u_t5", "u_t6", "u_t7", "u_t8"], "idempotencyKey": "ambpo-2026-10-29-team-2-trainees"}}
```

No guide covers teams, so the field names follow the skills (`traineeUids`) and the overview (name, managers, trainees). If a call returns `validation_failed`, I read `detail.issues`, fix the field name and resend with a new key.

### Step C. Rubric

No call. `rub_essentials` goes in every scenario's `rubricIds` and every preset. Building a rubric from the client's QA form is an app step (section 3).

### Step D. Personas (three, all Gulf Arabic)

The shop owner adapts the starter "Impatient power user who tried everything" and the mother adapts "Older customer who needs simple steps". Both starters are US English or Jordanian, so I write Gulf versions and keep their controls. The distrustful customer is new. Bodies are profiles in the third person with no call-specific facts. City, currency and dialect live here and nowhere else.

**D1. Impatient online-shop owner (difficulty 4)**

```json
{
  "tool": "personas_save",
  "input": {
    "properties": {
      "name": "Impatient online-shop owner who works from home",
      "language": "ar",
      "lexicon": "gulf",
      "gender": "male",
      "ageRanges": ["35-44"],
      "difficulty": 4
    },
    "advanced": {
      "traits": {"patience": 1, "skepticism": 4, "talkativeness": 4, "politeness": 2, "decisiveness": 5},
      "mood": "irritated",
      "interruption": "often",
      "escalationThreshold": 3
    },
    "body": "# Impatient online-shop owner who works from home\n\n## Who they are\n\nFaisal, 38, runs a small online shop that sells phone accessories from the spare room of his house in Riyadh. Orders, customer chats and card payments all run over his home fiber line, which costs about 300 riyals a month. He has no backup line except his phone's mobile data. He has been a subscriber for four years and has called the provider's helpdesk several times before.\n\n## Goals and motivations\n\nKeep the shop online through the day and the evening rush. He wants a cause and a time, not sympathy, and he judges a provider by how little of his time it wastes.\n\n## Pains and objections\n\nHe hates repeating his account number and his story to each new agent. He hates scripted steps he has already done, such as restarting the box. He believes providers hide behind «the system» and says so.\n\n## Decision style\n\nDecides fast and expects the agent to do the same. Wants one person who owns the problem. Asks for a manager after a few unhelpful answers.\n\n## How he talks on the phone\n\nFast, loud at the start, short sentences, in Gulf Arabic with a Najdi flavor (الحين، أبغى، وش). He cuts in the moment he hears a familiar script line: «أيوه أيوه عرفت، جرّبت هالشي». He repeats the question until he gets a direct answer. He calms down only when the agent skips the script, says plainly what is wrong and gives a time he can plan around.\n\n## What wins him over\n\nAn agent who listens to what he already tried, asks one sharp question, names the cause and gives a time with a way to be told. Tone alone does not move him; he needs something he can check, such as a reference number or a status the agent reads out. He is lost by «please be patient», by a script read aloud and by a transfer.\n\n## A typical line\n\n«كل مرة نفس الكلام! أبغى أعرف وش المشكلة بالضبط ومتى ترجع الخدمة، الحين مو بعدين.»",
    "idempotencyKey": "ambpo-2026-10-29-persona-shop-owner"
  }
}
```
Result: `$P_SHOP`.

**D2. Distrustful customer who has heard it all before (difficulty 5)**

```json
{
  "tool": "personas_save",
  "input": {
    "properties": {
      "name": "Distrustful customer who has heard it all before",
      "language": "ar",
      "lexicon": "gulf",
      "gender": "female",
      "ageRanges": ["45-54"],
      "difficulty": 5
    },
    "advanced": {
      "traits": {"patience": 2, "skepticism": 5, "talkativeness": 4, "politeness": 3, "decisiveness": 4},
      "mood": "suspicious",
      "interruption": "sometimes",
      "escalationThreshold": 4
    },
    "body": "# Distrustful customer who has heard it all before\n\n## Who they are\n\nHuda, 49, is the accounts manager of a family clinic in Jeddah. She works from home two days a week and handles every household bill and every call to a provider herself. She has been a subscriber for six years, pays about 250 riyals a month, has eight months left on her contract and knows the early-cancellation terms. She keeps a notebook with the name, time and reference number of every call she makes to the provider.\n\n## Goals and motivations\n\nA permanent fix, one named person who is accountable, and fair treatment for a loyal customer. She does not want to be a case; she wants to be remembered.\n\n## Pains and objections\n\nPromises that were never kept, tickets closed without a visit, and being told «it is resolved» when it is not. She believes the first answer is usually a way to end the call.\n\n## Decision style\n\nMethodical. She accepts a claim only with a reference or a date behind it and does not take «soon». Her husband approves any change of provider, but she makes the case to him.\n\n## How she talks on the phone\n\nGulf Arabic with a Hijazi flavor (دحين، إيش، أبغى). Her voice stays calm and gets colder and slower as she doubts. She asks «من وين عرفت؟» and «طيب أثبت لي». She writes things down and reads them back: «خليني أكتب اسمك ورقم المرجع». Pressure and a raised tone make her shorter and less cooperative.\n\n## How fast she warms up, and what wins her\n\nSlowly. She warms up only when the agent owns the failure with specifics (what went wrong before, not a general apology), gives commitments with a date and a reference she can check, and does what was said. A generic apology or a transfer makes it worse.\n\n## A typical line\n\n«دحين تقول لي بكرة؟ أنا سمعت هالكلام قبل ثلاث مرات. اكتب لي رقم المرجع وأنا بسجّله.»",
    "idempotencyKey": "ambpo-2026-10-29-persona-distrustful"
  }
}
```
Result: `$P_DISTRUST`.

**D3. Patient, non-technical mother (difficulty 2)**

```json
{
  "tool": "personas_save",
  "input": {
    "properties": {
      "name": "Patient non-technical mother who needs simple steps",
      "language": "ar",
      "lexicon": "gulf",
      "gender": "female",
      "ageRanges": ["55-64"],
      "difficulty": 2
    },
    "advanced": {
      "traits": {"patience": 4, "skepticism": 2, "talkativeness": 4, "politeness": 5, "decisiveness": 2},
      "mood": "confused",
      "interruption": "rarely",
      "escalationThreshold": 9
    },
    "body": "# Patient non-technical mother who needs simple steps\n\n## Who they are\n\nUmm Khalid, 58, is a homemaker in Dammam. The bills are in her name. She has three grown children, and the home line is used for family video calls, TV and her children's phones. She does not know router words: she says «the box» and «the Wi-Fi». Her youngest son sets everything up when he is home.\n\n## Goals and motivations\n\nKeep the family connected and not be a bother to anyone.\n\n## Pains and objections\n\nShe is afraid of pressing the wrong button and making it worse. She is embarrassed to say she did not understand, so she says yes anyway.\n\n## Decision style\n\nHesitant. She asks her son or her husband before she changes anything. She follows steps well when each one is given alone and the agent waits for her.\n\n## How she talks on the phone\n\nWarm, polite Gulf Arabic, a little chatty, with small stories. She says «الله يعافيك» and «يا ولدي». «إي» can mean she is not sure. When she is lost she slows down and says «عيد علي».\n\n## What wins her over\n\nShort plain words, one step at a time, and a question after each step (what do you see now?). An agent who tells her it is not her fault. She is lost by jargon (router, SSID), by long lists and by fast speech.\n\n## A typical line\n\n«الله يعافيك يا ولدي، أنا ما أفهم في هالأمور، قل لي وش أسوي خطوة خطوة.»",
    "idempotencyKey": "ambpo-2026-10-29-persona-mother"
  }
}
```
Result: `$P_MOTHER`.

### Step E. Scenarios (three new, all neutral: no dialect, nationality, currency or city)

**E1. Outage with a red light (area outage; the customer touched the cable)**

```json
{
  "tool": "scenarios_save",
  "input": {
    "properties": {
      "title": "Internet down since last night, red light on the fiber box",
      "direction": "inbound",
      "customerSpeaksFirst": false,
      "maxDurationSec": 480,
      "rubricIds": ["rub_essentials"]
    },
    "instructions": "## SITUATION\n\nYour home internet stopped working last night at about 9 pm. Every device shows no connection. You want to know what is wrong and when it will work again, and you do not want to lose another day.\n\n## FACTS (reveal each only when asked, one per turn)\n\n- The small box on the wall where the cable comes in has a red light blinking and the green light is off (when asked what lights the box shows)\n- It stopped at about 9 pm yesterday and had worked normally for months before (when asked when it started or whether it worked before)\n- You restarted the box and the router twice by pulling the power for a minute, and nothing changed (when asked what you have tried)\n- Your neighbor in the next flat told you this morning that his internet is down too (when asked whether anyone nearby has the same problem)\n- Your account number is 40213377 and the service address is flat 12 in your building (when asked to verify your identity or give the account number)\n\n## DO, IN ORDER\n\n1. Say the internet has been down since last night and ask what is wrong.\n2. Answer the agent's checks one at a time.\n3. Ask when it will work again and whether someone has to come to your home.\n4. Accept an honest estimate with a way to be told when it is back. Do not accept «wait and see» with no time.\n\n## REACTIONS\n\n- \"I did not move anything. Are you saying this is my fault?\" (when the agent asks whether anything was touched or moved, in a tone that sounds like blame)\n- \"Do I really have to stay home all day waiting for a technician?\" (when the agent offers a technician visit)\n- \"So you are telling me nothing can be done?\" (when the agent only says there is an outage and gives no time)\n- You relax and become friendly when the agent says plainly that it is not your fault.\n\nThings that may come up during the call, when the moment fits:\n- You ask whether you will pay for the days without service.\n- You say your phone's mobile data is the only thing working, and you ask whether that is the best you can get.\n\n## HIDDEN TRUTH (something you know and never volunteer)\n\nAn hour before you called, you pulled the cable out of the box and pushed it back in to see if it would help. You are worried you broke it. You say so only if the agent asks whether anything was touched or unplugged and has spoken to you without blame.\n\n## HOW IT ENDS\n\nYou thank the agent and hang up once the agent has checked and told you there is an outage in your area, given a restoration time and what happens if it is not back by then, and told you how you will be informed. You end the call irritated if the agent books a technician visit without checking for an outage, or if all you hear is «please wait» with no time.",
    "expectations": "## The real cause (the customer cannot know it; the agent finds it on their side)\n\nA cut on the fiber feeder line that serves the customer's building and the buildings next to it, starting at about 8:50 pm yesterday. It is already in the area outage list with an estimated restoration of about 2 pm today. The customer pulling the cable did not cause it. The agent only finds this by checking the area outage status for the service address, not by guessing.\n\n## A good call\n\nThe agent verifies identity, asks what the lights show and what was already tried (and does not make the customer repeat the restarts), then checks for a known outage at the service address before anything else. It tells the customer plainly that this is an area outage, gives the restoration time the system shows and says it is an estimate, says what happens if it is not back by then (a callback or an automatic follow-up, with a reference number), and says how the customer will be told. It asks whether anything was touched or unplugged without blame and reassures the customer that the cable was not the cause. No technician visit is booked. If the customer asks about a credit for the downtime, the agent states what the client's policy allows and does not invent an amount.\n\nFailure: booking a technician visit, or sending the customer through another reset or a new box, as the fix. Also a failure: blaming the customer, giving a restoration time the system does not show, or promising a credit outside policy.\n\n## Pitfalls to watch for\n\nRunning the full reset script after the customer said they did. Asking the customer to buy equipment. «It will be fixed within the hour» with no data behind it. Opening a ticket before checking for an outage. Closing the call without telling the customer how they will be informed.",
    "idempotencyKey": "ambpo-2026-10-29-scenario-red-light"
  }
}
```
Result: `$S_REDLIGHT`.

**E2. Slow Wi-Fi in the evenings**

```json
{
  "tool": "scenarios_save",
  "input": {
    "properties": {
      "title": "Wi-Fi slow in the evenings, fast next to the router",
      "direction": "inbound",
      "customerSpeaksFirst": false,
      "maxDurationSec": 480,
      "rubricIds": ["rub_essentials"]
    },
    "instructions": "## SITUATION\n\nFor two weeks, video calls and streaming have been lagging and buffering in the evenings, mostly in the bedrooms at the far end of your home. You pay for a fast plan and expect it to work in the whole home. You would like it fixed without a technician visit if that is possible.\n\n## FACTS (reveal each only when asked, one per turn)\n\n- Your plan is 500 Mbps. A speed test on your phone standing next to the router gives about 480, and in the far bedroom about 12 (when asked about your plan, or whether you ran a speed test, or where it is slow)\n- The router sits inside a closed metal cabinet in the hallway, next to the front door (when asked where the router is)\n- About fourteen devices are connected: phones, two TVs, a games console, tablets and a smart speaker (when asked how many devices use the Wi-Fi)\n- It is worst between 8 and 11 pm and fine in the morning (when asked when it happens or whether it is always slow)\n\n## DO, IN ORDER\n\n1. Say the Wi-Fi is slow in the evenings and ask for it to be fixed.\n2. Answer the agent's questions one at a time and try the simple steps the agent gives you. Report what happened after each one.\n3. Ask whether you need a technician or a new device, and what that would cost.\n4. Accept a short list of steps with a way to check it worked. Refuse to pay for anything before the free steps have been tried.\n\n## REACTIONS\n\n- \"I pay for 500, so why am I getting 12?\" (when the agent says the line is fine or the speed at the router is fine)\n- \"The cabinet is there on purpose. I do not want the router sitting out in the hall.\" (when the agent suggests moving the router)\n- \"Just send someone.\" (when the agent asks for more than two steps over the phone)\n\nThings that may come up during the call, when the moment fits:\n- You mention that your son's online game lags the most, and you ask whether he should play wired.\n- You ask whether you should buy a booster from a shop, and what the company offers.\n\n## HIDDEN TRUTH (something you know and never volunteer)\n\nA month ago, on a neighbor's advice, you bought a cheap Wi-Fi booster and plugged it into the hallway socket. You think it is not worth mentioning. You say so only if the agent asks whether you added any other device, booster or extender.\n\n## HOW IT ENDS\n\nYou thank the agent and hang up once the agent has separated the speed next to the router from the speed in the far room, found the closed cabinet and the booster, given you concrete steps to try tonight (for example moving the router to an open shelf and unplugging the booster for a test), and told you what happens if it is not better after that. You end the call annoyed if the agent books a technician at once, offers a faster plan, or asks you to pay for something before the free steps.",
    "expectations": "## The real cause (what a good call finds)\n\nThe line and the router are healthy: the speed next to the router matches the plan. The problem is coverage and congestion inside the home: the router is in a closed metal cabinet, and a booster the customer added is holding devices on a weak link, worst in the evening when fourteen devices are in use. The agent finds this only by asking where the router is and whether anything was added.\n\n## A good call\n\nThe agent asks for a speed test next to the router and in the far room before anything else, concludes the line is fine, asks where the router sits and how many devices use it, and asks whether anything else was added to the network. It gives concrete steps the customer can do on the call (move the router out of the cabinet or open the cabinet, unplug the booster and test again) and checks the result with the customer. If the customer refuses to move the router, the agent offers another way (open the door, a higher open shelf, a wired connection for the console) and does not push. It says what happens if the speed is not better (a dated callback or a dated technician visit).\n\nFailure: selling a faster plan, which does not fix this. Also a failure: booking a technician as the first move, or asking for a factory reset before asking where the router sits. A paid extender may be mentioned only after the free steps, only if the client offers one, and without an invented price.\n\n## Pitfalls to watch for\n\nReading a generic Wi-Fi script. Treating «I pay for 500» as a billing problem. Arguing about the speed test. Not asking about added devices. Ending without a way for the customer to confirm it worked.",
    "idempotencyKey": "ambpo-2026-10-29-scenario-slow-wifi"
  }
}
```
Result: `$S_WIFI`.

**E3. Third outage this month (the hard call)**

```json
{
  "tool": "scenarios_save",
  "input": {
    "properties": {
      "title": "Third outage this month, wants a firm date and compensation",
      "direction": "inbound",
      "customerSpeaksFirst": true,
      "openingLine": "This is the third time this month my internet has gone down. I want to know what you are going to do about it.",
      "maxDurationSec": 540,
      "rubricIds": ["rub_essentials"]
    },
    "instructions": "## SITUATION\n\nYour internet has dropped completely three times this month: on the 4th, on the 15th and this morning at about 6 am. Each time it came back by itself after some hours. You want it fixed for good, someone who owns the problem, and compensation for the lost days. You are close to leaving.\n\n## FACTS (reveal each only when asked, one per turn)\n\n- The outages: the 4th for about five hours, the 15th for the whole day, and this morning from 6 am until now (when asked when it happened or how long)\n- You called on the 15th and were told a ticket was opened. Nobody contacted you. The SMS you received had the number 7731902 (when asked about earlier calls or tickets)\n- Each time, the light on the box turned red and later went back to green without you doing anything (when asked what you saw or what you did)\n- You have been a customer for three years and never had problems before this month (when asked how long you have had the service)\n\n## DO, IN ORDER\n\n1. Say it is the third time this month, using your own words for the opening.\n2. Ask what the earlier ticket says and why nobody called you.\n3. Ask for a fixed date for a permanent repair and for one person who owns it.\n4. Ask for compensation for the lost days.\n5. Accept only a dated technician visit or escalation with a reference number, a named owner, and a straight answer on compensation.\n\n## REACTIONS\n\n- \"Every time you say a ticket is opened, and the last one did nothing.\" (when the agent says they will open a ticket)\n- \"So you want me to wait another week?\" (when the agent offers a visit more than three days away)\n- \"I do not want a discount on a service I am not getting. I want it to work.\" (when the agent offers a credit before a fix)\n- You calm down a little when the agent takes responsibility in specifics, and you get colder if you hear a general apology.\n\nThings that may come up during the call, when the moment fits:\n- You ask for a manager. If the agent takes it on with confidence, you accept that. If the agent just transfers, you get angry.\n- You say another provider's salesperson called you last week.\n\n## HIDDEN TRUTH (something you know and never volunteer)\n\nYou have already asked another provider for an installation date, and you will cancel if you are not given a firm repair date today. You say so only if the agent asks whether you are thinking of leaving, or after you hear «we will get back to you» a second time.\n\n## HOW IT ENDS\n\nYou agree to stay and end the call calmly once you have a dated technician visit, a reference number, the name of who owns the case, a time by which you will hear from them, and an honest answer on compensation. You say you will cancel and ask how to do it if you hear «we will call you back» without a date, or any promise like the ones you have heard before.",
    "expectations": "## The real cause (the customer cannot know it; the agent finds it on their side)\n\nThe line from the street cabinet to the customer's home has a degraded connection, which drops the service for hours and then recovers. The ticket from the 15th (7731902) was closed as «service restored» without a technician visit, so there was no repair and no follow-up call. The agent finds this by reading the ticket history on the account before asking the customer to explain again. Another reset or a remote ticket will not fix it. A technician visit is needed.\n\n## A good call\n\nThe agent apologizes for the missed callback without excuses and reads the account history first. It finds the ticket from the 15th, says honestly that it was closed without a visit, and books a technician visit with a date and a time window (the earliest available, said aloud). It escalates the case as a repeat fault, gives a reference number and the name or team that owns it, and says by when the customer will hear back. It asks whether the customer is thinking of leaving. On compensation it states what the client's policy allows for outages of this length and logs the credit request as the policy says; it does not invent or promise an amount. It handles the request for a manager by owning the issue instead of transferring.\n\nIf the policy gives no compensation for outages of this length, the right answer is an honest refusal with a route to escalate, not an invented credit.\n\nFailure: opening another plain ticket with no visit, a callback with no time, or a credit promised outside policy.\n\n## Pitfalls to watch for\n\nOffering a credit before a fix. Arguing about what the earlier agent said. Asking the customer to restart the box again. Transferring at the first «I want a manager». Offering a visit more than three days away without saying why or offering an earlier option. Not asking about cancellation.",
    "idempotencyKey": "ambpo-2026-10-29-scenario-third-outage"
  }
}
```
Result: `$S_THIRD`.

Before the presets, I check each scenario text once against the writing-scenarios check: no persona, dialect, nationality, currency or city; every fact has its revealing question; each hidden truth is the customer's own; company-side causes are in `expectations`.

### Step F. Presets (five, recommended for both teams)

Every preset uses `"kind": "recommended"`, `"rubricIds": ["rub_essentials"]`, `"teamIds": ["$TEAM1", "$TEAM2"]`. The titles show the order. Each save pins the current versions.

```json
{"tool": "presets_save", "input": {"kind": "recommended", "title": "Outage 1 · Internet down, son's video call tonight × patient mother", "tags": ["outage", "rung-1"], "personaId": "$P_MOTHER", "scenarioId": "$S_SON", "rubricIds": ["rub_essentials"], "teamIds": ["$TEAM1", "$TEAM2"], "idempotencyKey": "ambpo-2026-10-29-preset-outage-1"}}
```
```json
{"tool": "presets_save", "input": {"kind": "recommended", "title": "Outage 2 · Red light on the fiber box × impatient shop owner", "tags": ["outage", "rung-2"], "personaId": "$P_SHOP", "scenarioId": "$S_REDLIGHT", "rubricIds": ["rub_essentials"], "teamIds": ["$TEAM1", "$TEAM2"], "idempotencyKey": "ambpo-2026-10-29-preset-outage-2"}}
```
```json
{"tool": "presets_save", "input": {"kind": "recommended", "title": "Outage 3 · Third outage this month × distrustful customer", "tags": ["outage", "rung-3", "top-rung"], "personaId": "$P_DISTRUST", "scenarioId": "$S_THIRD", "rubricIds": ["rub_essentials"], "teamIds": ["$TEAM1", "$TEAM2"], "idempotencyKey": "ambpo-2026-10-29-preset-outage-3"}}
```
```json
{"tool": "presets_save", "input": {"kind": "recommended", "title": "Wi-Fi 1 · Slow Wi-Fi in the evenings × patient mother", "tags": ["slow-wifi", "rung-1"], "personaId": "$P_MOTHER", "scenarioId": "$S_WIFI", "rubricIds": ["rub_essentials"], "teamIds": ["$TEAM1", "$TEAM2"], "idempotencyKey": "ambpo-2026-10-29-preset-wifi-1"}}
```
```json
{"tool": "presets_save", "input": {"kind": "recommended", "title": "Wi-Fi 2 · Slow Wi-Fi in the evenings × impatient shop owner", "tags": ["slow-wifi", "rung-2", "top-rung"], "personaId": "$P_SHOP", "scenarioId": "$S_WIFI", "rubricIds": ["rub_essentials"], "teamIds": ["$TEAM1", "$TEAM2"], "idempotencyKey": "ambpo-2026-10-29-preset-wifi-2"}}
```

### Step G. Verify

```json
{"tool": "presets_list", "input": {"kind": "recommended"}}
```
```json
{"tool": "teams_list", "input": {}}
```

Done means: five recommended presets, each with both team ids; each team lists its lead and four trainees; every preset pins the current version of its persona, scenario and `rub_essentials`.

### Step H. After the first week (not now; there are no drills yet)

When the owner says trainees have run the easiest drill of each call type:

```json
{"tool": "stats_team", "input": {"teamId": "$TEAM1"}}
```
```json
{"tool": "stats_team", "input": {"teamId": "$TEAM2"}}
```
Then, per trainee the leads want to look at (uids from `teams_list`):

```json
{"tool": "stats_progress", "input": {"uid": "u_t1", "timeZone": "Asia/Amman"}}
```

I read each number with `reading-results`: only counted calls (ended after going live), same preset and same versions for any comparison, and three counted calls or fewer is an anecdote. I report each trainee against the proposed bar with the drills behind it. Every verdict stays **provisional** until the owner confirms the bar, and "not enough data" is the verdict for a rung with too few counted calls. For coaching I use `drills_list` filtered to the trainee, then `evaluations_get` on a recent drill, and quote the moment and the next drill to run.

---

## 3. What I tell the owner at the end

> Your workspace is set up. Here is what I made.
>
> **Teams (2):** Helpdesk team 1 (lead `u_lead1`, trainees `u_t1` to `u_t4`) and Helpdesk team 2 (lead `u_lead2`, trainees `u_t5` to `u_t8`). Rename or re-split them whenever you like.
>
> **Customers (3, all Gulf Arabic):** Impatient online-shop owner (Riyadh, difficulty 4), Distrustful customer who has heard it all before (Jeddah, difficulty 5), Patient non-technical mother (Dammam, difficulty 2).
>
> **Calls (3 new, plus 1 Minerva starter):** Internet down since last night with a red light on the fiber box, Wi-Fi slow in the evenings, Third outage this month with a request for a firm date and compensation, and the starter "Internet down, her son video-calls tonight".
>
> **Drills both teams now see (5):** Outage 1, 2 and 3, and Wi-Fi 1 and 2, in that order, all scored on "Customer call essentials". Tell the leads to use these five. The three default drills from the Technical support starter use US English and Jordanian customers, not Saudi ones.
>
> **How the leads see who is ready.** The team view in the app shows each team's calls, averages and the calls still to review. I also read it for you on request. My proposed bar, **provisional until you confirm it**: the latest counted call on every drill scored 70 or higher, and the top drill of each call type (Outage 3, Wi-Fi 2) scored 70 or higher twice. A trainee with fewer counted calls is "not enough data".
>
> **Week one:** each trainee runs Outage 1 and Wi-Fi 1 first, then works up. Leads review the calls and I help with the coaching notes.
>
> **What only you can do, in the app:**
> 1. Check the workspace has enough credits for the first week: every counted call uses one.
> 2. If the client has its own QA form, send it to me. I will write the line-by-line mapping, and you build it under Library, Rubrics. Until then the default rubric scores the calls.
> 3. Trainees start the calls themselves from the app. I cannot start a call.
> 4. Invites, roles and removing members are also app steps. If more people join, tell me and I will add them to a team.
>
> **What I still need from you:** the client's name, its outage-credit rule, how fast it books a technician visit, which tool shows area outages, and whether 70 is the right bar. With these I tighten the calls and re-save the five drills so trainees get the new versions. Also, the Saudi dialect is the general Gulf one: tell me after the first calls if your agents need a different spoken accent.
>
> **Note for later:** if you take on other clients, give each its own workspace (in the app) so libraries, scores and access stay apart.

