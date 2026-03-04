# Retro: Second Brain Starter — Full Build
**Prompt range:** P-001 → P-003
**Date:** 2026-03-01

## Metrics
- **Total turns:** 3
- **Productive: 2 (67%)** — 2 clean-execution
- **Waste: 0 (0%)**
- **Neutral: 1 (33%)** — 1 planning

## What Happened

| Turn | Tag | Summary |
|------|-----|---------|
| P/R-001 | planning | SPS init, 11-step plan, repo name brainstorm (4 options) |
| P/R-002 | clean-execution | Built all 12 files in one turn — MCP server, SQL, setup.sh, docs, README, setup prompt |
| P/R-003 | clean-execution | External code review: triaged 13 findings, fixed 10, skipped 3 |

## Analysis

This is what a project looks like **after** you've already built the thing once. Cloud-mcp was the learning project; second-brain-starter was the generalization. The metrics reflect that:

- **Zero waste turns.** No SDK version hunting, no auth debugging, no process catch-up.
- **One planning turn, then pure execution.** The plan was informed by cloud-mcp's completed milestones.
- **12 files in one turn.** Possible because every pattern (MCP server structure, SQL schema, setup flow) was already proven in cloud-mcp.

The 67% productive rate is slightly misleading — with only 3 turns, one planning turn pulls the percentage down. The real signal: **2 turns of building produced a complete, review-hardened template repo.** That's the compound return on cloud-mcp's 13 turns.

## Optimal Path

Already near-optimal. The only improvement:

1. **Include code review findings in the initial build prompt.** The 10 fixes from P-003 (byte-length check, path traversal guard, TOCTOU fix) could have been specified upfront since they were known patterns from cloud-mcp's code review. That would reduce this to a 2-turn project.

**Estimated optimal turns: 2** (vs 3 actual — already tight)

## Key Decisions Worth Documenting

| Decision | Choice | Why |
|----------|--------|-----|
| Onboarding path | Setup prompt (paste into Claude) over README | Target user is non-developer; Claude guides them through setup |
| MCP server | Generalized from cloud-mcp, dropped sync.ts | Template shouldn't assume GitHub sync; users add their own sources |
| Setup script | Bash with `gum` for interactive prompts | Friendly UX for non-technical users; degrades to plain prompts without gum |
| Security | Path traversal guard, byte-length check, single-query remove | Bake security in from the start rather than hardening later |

## Playbook Candidates

1. **Build the learning project first, then generalize.** Cloud-mcp → second-brain-starter took 3 turns because all patterns were proven. Don't template prematurely — build one real instance first. (Source: entire project arc)
2. **Include known hardening patterns in the initial build prompt.** If you've already done a code review on the source project, feed those findings into the template build. Don't repeat the review cycle. (Source: P-003 could have been avoided)
3. **Setup prompts > README for non-developer audiences.** A prompt they paste into Claude gives guided, interactive onboarding. A README gives a wall of text. Know your audience. (Source: P-001 design decision)
