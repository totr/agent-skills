# Skill Authoring Guidelines

## Purpose

This repository contains portable Agent Skills distributed through the `skills` CLI. Follow the [Agent Skills specification](https://agentskills.io/specification).

Write all documentation, skill instructions, examples, and code comments in English.

## Repository Layout

```text
skills/<skill-name>/
├── SKILL.md       # Required entry point for an installable skill
├── references/   # Optional supporting documentation
├── scripts/      # Optional executable helpers
└── assets/       # Optional templates, examples, and static resources
```

- Keep one skill per directory under `skills/`.
- Create supporting directories only when they contain useful files.
- Keep each skill self-contained. Do not depend on files outside its directory or assume other skills are installed.
- Keep the root `README.md` focused on user-facing installation, usage, available skills, and updates. Put authoring instructions in this file.
- Place GitHub Actions workflows in `.github/workflows/` when needed.

## SKILL.md Format

Start with YAML frontmatter followed by Markdown instructions:

```markdown
---
name: skill-name
description: Describe what the skill does and the specific situations in which an agent should use it.
---

# Skill Title

## Workflow

1. Identify the inputs and requirements.
2. Perform the task using the relevant bundled resources.
3. Verify the result and present the expected output.
```

- `name` must match the directory name, be 1–64 characters long, and use lowercase ASCII letters, digits, and single hyphens. Do not start or end with a hyphen.
- `description` must be non-empty and at most 1,024 characters. Explain both the capability and when to invoke it; avoid vague descriptions or overly broad triggers.
- Add optional frontmatter only when useful. Use `compatibility` to document specific runtime or environment requirements.
- Do not invent license information or promise compatibility that has not been verified.

## Instruction Quality

- Give each skill a focused purpose and a clear expected result.
- State required inputs, actionable steps, relevant edge cases, and how to verify success.
- Include concrete examples when they clarify ambiguous behavior or output formats.
- Keep `SKILL.md` concise and under 500 lines. Move detailed material into focused reference files.
- Link directly to supporting files from `SKILL.md` and explain when to read or use them. Avoid long chains of references.
- Use paths relative to the skill directory, such as `references/checklist.md` or `scripts/render.py`.

## Portability

- Maintain a single source for all supported agents. Do not create agent-specific copies under `.claude/`, `.codex/`, or `.opencode/`.
- Describe operations in agent-neutral terms, such as “read the file” or “search the repository,” instead of requiring a particular agent's internal tool names.
- Do not assume a specific model, agent API, subagent mechanism, or experimental tool-permission field is available.
- Explicitly document any required MCP server, external service, network access, executable, or runtime version. The `skills` CLI installs skill files; it does not make these dependencies available automatically.
- Make script invocation independent of the consumer's working directory by explaining that bundled paths are relative to the installed skill directory.

## Scripts and Resources

- Add executable helpers only when they make the task more reliable or reproducible.
- Document inputs, outputs, dependencies, and any files the script creates or modifies.
- Use clear errors for missing dependencies and invalid inputs.
- Keep templates and static examples in `assets/`; keep explanatory documentation in `references/`.

## Verification

Before completing a skill change:

1. Check frontmatter, directory naming, and every referenced local path.
2. Check that the skill works as a standalone directory without repository-only resources.
3. Exercise bundled scripts with representative inputs and relevant failure cases.
4. Review a task that should activate the skill and a related task that should not. For behavioral changes, exercise representative tasks in the intended agents when available.
5. If `skills-ref` is available, run `skills-ref validate skills/<skill-name>` for each changed, implemented skill. Do not validate placeholders as complete skills.
6. Update user-facing documentation when availability, installation, requirements, or usage changes.

Report what was actually checked and any checks that could not be run. Do not claim cross-agent compatibility based on file-format validation alone.
