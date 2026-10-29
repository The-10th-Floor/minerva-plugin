---
name: setting-up-a-workspace
description: Use when setting up or reshaping a Minerva workspace for a team, a training program, a new hire class or a BPO client program, or when someone asks to get their agents practicing on Minerva.
---

# Setting up a workspace

The goal is a **library grid**: for each call type the team takes, a few customers (personas) crossed with a few calls (scenarios), scored on the right rubric, and handed to each team as ready drills (presets). Run `getting-started` first.

## 1. Read before you write

1. `account_get`, then `teams_list`, `personas_list`, `scenarios_list`, `rubrics_list`, `presets_list`. Starters picked at sign-up are already in the library and carry a `templateId`.
2. Match the brief to the starter sets. Minerva ships three, each with three personas, scenarios and presets: **customer service** (food delivery), **technical support** (a helpdesk for home internet, Wi-Fi and business software) and **sales and telemarketing**. List the starters that fit from `writing-personas/starters.md` and `writing-scenarios/starters.md`; a fitting starter is the first row of the grid. A starter missing from the library is added in the app (Library, New, from a template), so the plan asks the person to add that set first, then you adapt it with get and save. Starter scenarios carry no dialect, so a persona in the callers' dialect plays them as they are (check any gender the text assumes).
3. Ask what you cannot see: the call types, the callers' country and language, the hard moments team leads name, how the floor's QA form scores a call, and who the trainees are.

## 2. Plan the grid, then confirm it

Write the plan as a table before saving anything: one row per call type, its scenarios, the personas that play them, the difficulty ladder (start at 2 or 3, finish at 4 or 5) and the rubric. Personas and scenarios are separate rows: any persona can play any scenario, and the preset is where a pair is chosen. The first save waits for the person's yes to the plan.

Size: three to five scenarios per call type and three customers cover most programs. A plan caps the library; a save past the cap returns `library_limit`, so build the rows that matter most first.

A BPO with several client programs keeps one workspace per client program, so each client's library, scores and access stay apart.

## 3. Build in this order

1. **Teams**: an owner runs `teams_create` per group of trainees with its managers, then `teams_update` with `traineeUids`. Uids come from `teams_list`; people join by invite in the app first.
2. **Rubrics**: pick one per call type with `choosing-rubrics`. Mapping a QA form gives the person a rubric to build in the app; the default rubric judges until then.
3. **Personas and scenarios**: with `writing-personas` and `writing-scenarios`.
4. **Presets**: one per pair the team should run, assigned to its teams (`building-presets`).

Ask before any tool that needs `confirm: true`.

## 4. Hand over

Done when every team in the plan sees at least one recommended preset per call type, every preset pins the current versions, and the person has the list of what you made and what still needs the app (invites, rubric building, credits). First week: each trainee runs the easiest preset of each call type, then team leads review with `coaching-from-drills`.
