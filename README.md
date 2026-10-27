# Agent Skills

Reusable skills for coding agents, installed with the [skills CLI](https://github.com/vercel-labs/skills).

Repository: [totr/agent-skills](https://github.com/totr/agent-skills).

## Available Skills

No installable skills are available yet.

## Installation

Once skills are available and this repository is published on GitHub, use the commands below to install them.

Requires Node.js 22.20 or later.

Run from the project where you want to use the skills:

```sh
npx skills add totr/agent-skills
```

Follow the prompts to select skills and target agents, such as Claude Code, Codex, or OpenCode.

To install skills globally for use across projects:

```sh
npx skills add totr/agent-skills -g
```

## Usage

After installation, ask your agent to perform a task covered by an installed skill. Each skill describes when it should be used; discovery and invocation depend on the agent.

List installed skills:

```sh
npx skills list
```

## Updates

Check for available updates and apply them:

```sh
npx skills check
npx skills update
```

## Removal

```sh
npx skills remove
```
