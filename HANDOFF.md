# Roadmap Skill — Handoff

Status as of 2026-06-30. Working on productizing the LN roadmap into a `/roadmap-update [client]` Claude skill for all retainer accounts.

## TL;DR
- LN roadmap is the working prototype: https://ln-roadmap-anatta.vercel.app/
- Repo: https://github.com/justinanatta/LN-Roadmap (local clone at `~/Documents/LN-Roadmap`)
- Sent FYIs to Mark, Matt, Nichole today via Slack. Waiting on reactions before scaling further
- Skill not built yet. Spec is ~80% locked, prompts need writing

## Where things live

- **Repo + live site**: `~/Documents/LN-Roadmap` → https://ln-roadmap-anatta.vercel.app/
- **Transcripts**: `~/Documents/llamanaturals/project/transcripts/`
- **Memory** (Claude Code, persists across sessions): `~/.claude/projects/-Users-justinon-Documents-llamanaturals/memory/`
  - `reference_roadmap_artifact_pattern.md` — encoding rules, palette, reusable weekly update prompt, hosting info
  - `project_renewal_outlook.md` — internal read on LN renewal (unlikely)
  - `feedback_no_label_shortforms.md` — full words on labels, no S5 / Invest. style shortforms

## Skill spec — locked

| Decision | Note |
|---|---|
| Command | `/roadmap-update [client]` — single skill, client as argument |
| Trigger | Manual. PM runs after a call. No auto-firing for now |
| Inputs | Granola transcript (needs Pro plan via MCP), Jira state (Atlassian MCP), anything PM forwards in chat |
| Output v1 | Just the gantt update. Shipped/changelog section comes later |
| Approval gate | Draft / public split. Skill writes to a draft branch → preview URL. PM reviews internally → merges to main → public Vercel deploy |
| Memory side-effects | Yes. Each run appends decisions + conversations + outcomes to `project-<client>-outlook.md`. Builds up over the contract window |
| Per-client config | `reference-<client>-roadmap.md` with Jira key, sprint cadence, contract dates, repo URL, live URL, draft URL, stakeholders |
| Slack | Manual only. No auto-scrape. PM forwards relevant threads |

## Skill spec — open

- Exact structure for the "decisions + conversations" block extracted from transcripts. Need to design this so it's queryable later
- Bootstrap flow for a brand new client: Jira epic pull + initial roadmap proposal + memory scaffolding generation
- Changelog/Shipped section: fold below the gantt, auto-derive from `done` bars, grouped by release version
- Whether the skill prompts PM to forward Slack threads or just relies on what they paste in

## Messages sent today

| Recipient | Role | Angle | Status |
|---|---|---|---|
| Mark | President of delivery | Retainer health, renewal artifact, PM efficiency, sales tool | Sent 12:55pm |
| Matt | Optimization director, Baron's boss | UXR landing visibility, test pipeline per account, optimization standardization | Sent |
| Nichole | PM director, my boss | PM team workflow, hours saved, standardization. Asked for her read before scaling | Sent |

Drafts of all three messages are in the Claude Code chat history from this session.

## LN roadmap — current state of the prototype

- Cart UI (LN-76, LN-78, LN-68) shipped in v1.5 on 6/30
- BOGO Custom Discount (LN-88) slipping to hot-fix 7/2. Sebi clarifying edge cases with Ritu
- Promotions lane split out from Cart Optimization. Links to LN-87 (UI Updates epic)
- HP Content Hierarchy (LN-99) flipped from IMPL to TEST after Brad's pushback in 6/30 weekly. Baron set up in Intelligems
- Checkout USP Icons (LN-95) blocked on Intelligems mobile-render bug
- Palette locked: dark muted Okabe-Ito (colorblind-safe). Background cool off-white #F4F6F8. Today line slate-blue Asana-style
- "Contract End" framing throughout, not "Renewal." Internal-only read on renewal lives in memory
- All bar labels use full words, no shortforms

## Next time you pick this up, start here

1. Check Slack for reactions from Mark / Matt / Nichole. Reply or address whatever came back
2. If Nichole gave direction, refine skill scope accordingly before building
3. Otherwise: start writing the skill prompts. Spec is mostly done, just needs implementation
4. Run a weekly roadmap update with whatever happened in the latest sync. Use the prompt in `reference_roadmap_artifact_pattern.md` section C

## Reusable prompts

- **Weekly update**: in `reference_roadmap_artifact_pattern.md` section C. Copy-paste into a new Claude conversation
- **Bootstrap for a new client**: not yet written. Sketched in the same memory file. Needs Jira MCP integration

## Gotchas to remember

- Git commits push under `justinon@Justins-MacBook-Air.local`. Fix with `git config --global user.email/user.name` when you have a minute
- Vercel auto-deploys from `main` on push. No build step. Pure static HTML
- Today line refreshes every minute via setInterval + on tab focus. Won't freeze on long-lived tabs
- Granola Pro plan needed for transcript MCP access. Pending budget confirmation from Mark
- The legacy claude.ai artifact at `964ced9b-135d-4053-9846-348c8e71c54b` is stale. Do not redeploy to it. Source of truth is the GitHub repo
