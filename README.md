# agents

Agent skills for the agentic coding loop. Works with [Codex CLI](https://github.com/openai/codex), [OpenCode](https://opencode.ai), and other agent harnesses that support the `.agents/skills/` convention.

## Install

```bash
git clone https://github.com/githits-com/agents ~/.agents
```

Codex CLI automatically discovers skills in `~/.agents/skills/` at startup.

## Skills

### `code-reviewer`

Reviews code changes and technical plans for bugs, regressions, performance, security, maintainability, and architectural soundness. Examines uncommitted changes and branch history, reads surrounding code for context, and produces a severity-ordered findings report. Runs as a read-only subagent — no code edits, no destructive git operations.

### `plan-reviewer`

Reviews technical plans before implementation and verifies completion against acceptance criteria. Checks for gaps in security, performance, testing strategy, UX, and developer experience. Also runs as a completion reviewer after implementation to verify acceptance criteria are met and flag minor deferred work that should be done now.

### `testing-specialist`

Helps create high-quality tests, fix flaky tests, and apply project testing conventions. Discovers project test patterns before acting, diagnoses common flaky test causes (race conditions, missing isolation, shared state), and writes or updates tests following established conventions. Has edit permissions to make changes directly.

## The Agentic Coding Loop

These skills support a four-step loop:

1. **Plan** — Define requirements and decompose into tasks
2. **Review plan** — `plan-reviewer` checks the plan before any code is written
3. **Build** — Agent implements autonomously
4. **Review build** — `code-reviewer` and `testing-specialist` check the result

Steps 2 and 4 always use a different model than the one that did the work — cross-model review catches what self-review misses.

## License

MIT