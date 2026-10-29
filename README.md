# Minerva plugin

Skills and the MCP connection that let your AI agent set up and run a [Minerva](https://minerva.thexfloor.com) workspace: AI customers, call scenarios, rubrics, ready drills for each team, and coaching from scored practice calls. For owners and managers of contact centers and BPOs.

## How to start

You need a Minerva account with the owner or manager role. Sign-in is OAuth in your browser: the plugin carries no API key, and your agent acts as you, with your role.

### Claude Code

```bash
claude plugin marketplace add AnasMK9/minerva-plugin
```

```bash
claude plugin install minerva@minerva-plugin
```

Then, in a session, run `/mcp`, pick `minerva`, sign in, and tick the workspaces and permissions to grant. The same two steps work inside a session as `/plugin marketplace add AnasMK9/minerva-plugin` and `/plugin install minerva@minerva-plugin`.

### Claude.ai and Claude Desktop

1. Open [Customize, Plugins](https://claude.ai/customize/plugins), then Add, Add marketplace, and enter `AnasMK9/minerva-plugin`. You can also download this repository as a zip and use Add, Upload plugin.
2. Add the Minerva plugin, open its Connectors tab, and connect `minerva`.

A plugin added here also reaches Claude Code on the same account. Without the plugin, add `https://minerva.thexfloor.com/api/mcp` as a custom connector, then upload the folders under `skills/` in Customize, Skills.

### ChatGPT and other MCP clients

Add `https://minerva.thexfloor.com/api/mcp` as a custom MCP server with OAuth ([ChatGPT's steps](https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt)). These clients do not load the skills; the server's own guides (`docs_get`) carry the rules there.

### First request

Ask your agent: "Set up our Minerva workspace for the helpdesk team." It reads your account, proposes a plan of customers, calls and drills, and builds it once you agree.

## Skills

| Skill | Your agent reaches it when |
| --- | --- |
| [`getting-started`](skills/getting-started/SKILL.md) | Connecting, starting Minerva work in a session, choosing a workspace, or a sign-in error |
| [`setting-up-a-workspace`](skills/setting-up-a-workspace/SKILL.md) | Setting up or reshaping a workspace for a team, program, hire class or BPO client |
| [`writing-personas`](skills/writing-personas/SKILL.md) | Creating or tuning an AI customer |
| [`writing-scenarios`](skills/writing-scenarios/SKILL.md) | Creating or editing a practice call |
| [`choosing-rubrics`](skills/choosing-rubrics/SKILL.md) | Choosing how calls are scored, explaining a score, or mapping a QA form |
| [`building-presets`](skills/building-presets/SKILL.md) | Giving a team ready drills, or after editing what a drill uses |
| [`querying-minerva`](skills/querying-minerva/SKILL.md) | Looking up library items, drills or people, or pulling numbers for a report |
| [`reading-results`](skills/reading-results/SKILL.md) | Interpreting a score, a scorecard, a drill status or a statistic, or comparing calls |
| [`coaching-from-drills`](skills/coaching-from-drills/SKILL.md) | Reviewing scores, deciding who is ready, or coaching a trainee |

In Claude Code they run on their own when a task matches, or by name, for example `/minerva:setting-up-a-workspace`.

## Data

The plugin itself stores nothing. Your agent reads and writes your Minerva workspace through `minerva.thexfloor.com`, as you, within the workspaces and permissions you granted at sign-in: the library (personas, scenarios, presets), teams, practice drills, scores and statistics. Inviting people, roles, credits, building rubrics and starting calls stay in the Minerva app. Each person is limited to 60 tool calls and 20 changes a minute.

## How the skills stay in step with Minerva

The skills carry what the server cannot: the setup workflow, judgment, the starter catalog with annotated examples, tuning recipes, and how to read results. Field rules, limits, the dialects a workspace serves and a worked example live in the server's guides, which your agent reads with `docs_get` before its first save and which change with the product. Each skill points there instead of copying them.

Minerva's repository keeps this plugin in its rules: a change to the guides, the starter templates or the MCP tool list updates these skills in the same week. Each release raises `version` in `.claude-plugin/plugin.json`; Claude Code picks it up through `/plugin marketplace update minerva-plugin`, or on its own once auto-update is on for this marketplace.

`testing/` holds the check behind each skill: the same brief run by an agent without the skills and with them. [TESTING.md](TESTING.md) has the results.

## License

[MIT](LICENSE)
