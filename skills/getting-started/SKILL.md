---
name: getting-started
description: Use when connecting an agent to Minerva, starting Minerva work in a new session, working across several Minerva workspaces, or when a Minerva tool returns unauthenticated or forbidden.
---

# Getting started with Minerva

Minerva is AI call practice for contact centers. A trainee phones an AI customer in a voice drill, an AI judge scores the call on a rubric, and a manager coaches from the scorecard. You work through Minerva's MCP tools as the person who signed in, with their role.

## Connect once

The `minerva` server is `https://minerva.thexfloor.com/api/mcp`. Sign-in is OAuth in the browser, with no API key.

| Client | Connect |
| --- | --- |
| Claude Code with this plugin | `/mcp`, pick `minerva`, sign in, tick the workspaces and permissions to grant |
| Claude.ai or Claude Desktop with this plugin | Customize, Plugins, Minerva, Connectors tab, Connect |
| Any other MCP client | Add the URL as a custom connector |

## Orient, every session

1. `account_get`: who you act as, and your role in each workspace. With several workspaces, pass `orgId` to every tool except `search` and `fetch`.
2. `docs_get` with no topic returns the overview. Before the first save of a kind, read its guide. The topics are exactly `overview`, `personas`, `scenarios`, `rubrics`, `presets`, `drills` and `stats`. The guides own the field rules, the dialects and call length this workspace serves, and a worked example. When a guide and a skill differ, the guide wins.
3. Match the task to a skill:

| Task | Skill |
| --- | --- |
| Set up or reshape a workspace for a team, program or client | `setting-up-a-workspace` |
| Create or tune an AI customer | `writing-personas` |
| Create or edit a call | `writing-scenarios` |
| How drills are scored, or a QA form to map | `choosing-rubrics` |
| Give a team ready drills | `building-presets` |
| Find drills, people or library items, or count anything | `querying-minerva` |
| Explain a score, a status or a statistic | `reading-results` |
| Review drills and coach people | `coaching-from-drills` |

## Roles

Owners do everything below, including creating and deleting teams. Managers write the library, put trainees in the teams they manage, and see those teams' drills. Trainees read the library and their own results.

## What stays in the app

Inviting and removing members, roles, workspace settings, credits, building or editing rubrics, adding starter templates (Library, New, from a template) and starting a call. Name the screen that does it and carry on with the rest.

## When a tool refuses

- `unauthenticated`: the sign-in expired or was revoked. Ask the person to reconnect (`/mcp` in Claude Code, the Connectors tab elsewhere).
- `forbidden`: this role cannot do it. Say who can.
- Any other code: the overview guide lists it with its fix.
