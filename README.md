# workflow-skills

Agent skills for the everyday work around the code and the writing, starting with your standup and community triage, in any IDE or AI agent that supports [Agent Skills](https://agentskills.io).

[![License: MIT](https://img.shields.io/github/license/Timonwa/workflow-skills)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-6E56CF)](https://agentskills.io)
[![GitHub stars](https://img.shields.io/github/stars/Timonwa/workflow-skills?style=flat)](https://github.com/Timonwa/workflow-skills/stargazers)
[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20me%20a%20coffee-support-FFDD00?logo=buymeacoffee&logoColor=black)](https://buymeacoffee.com/timonwa)

## Contents

- [The skill sets](#the-skill-sets)
- [How the skills work](#how-the-skills-work)
- [Install](#install)
- [Set up](#set-up)
- [Commands](#commands)
- [Contributing](#contributing)
- [Support](#support)

## The skill sets

Skills are grouped by the work they support.

| Set      | For                      | Install it if you                                                                |
| -------- | ------------------------ | -------------------------------------------------------------------------------- |
| `devrel` | Developer relations work | Post a daily standup, or look after issues and pull requests from your community |

## How the skills work

- Commands run only when you call them.
- To call one by name, type `$` and its name in Codex (`$daily-standup`), or `/` in Claude Code (`/daily-standup`, or `/devrel:daily-standup` with the plugin). In Claude Code, a command runs only when you type its `/` name. In other agents, ask for it by name.
- They read from GitHub through its command-line tool (`gh`) and report in the chat. They never comment, merge, close or post anything.
- Your GitHub handle and the orgs to watch come from the command's arguments or your project's `AGENTS.md`. Without either, the command asks once.
- Nothing is reported that GitHub didn't return, and nothing goes in your standup that you didn't confirm.

## Install

The commands call GitHub from the shell, so they need an agent that can run commands, such as Codex or Claude Code, not a chat app. First, install GitHub's command-line tool and sign in:

```shell
gh auth login
```

### Any IDE or AI agent

```shell
npx skills add Timonwa/workflow-skills
```

[`npx skills`](https://github.com/vercel-labs/skills) asks which skills to install and which agents to install them for — Cursor, GitHub Copilot, Codex, Gemini CLI, Claude Code and many more — and installs them in the current project. Add `-g` to install them for every project. To get the latest changes, run `npx skills update`.

To skip the questions, name your agents and take every skill. For example, for Codex and Claude Code in every project:

```shell
npx skills add Timonwa/workflow-skills -g -a codex -a claude-code --skill '*'
```

Without Node, copy the folders inside `plugins/devrel/skills/` into `.agents/skills/` in your project, or `~/.agents/skills/` for every project. Many agents read that folder. For the rest, use the skills folder your agent's docs name. To update, copy them again from the latest version of this repo.

### Claude Code as a plugin

Claude Code can also install the set as a plugin, which keeps the `devrel:` prefix:

```shell
/plugin marketplace add Timonwa/workflow-skills
/plugin install devrel@workflow-skills
```

When it asks for a scope, pick one:

- **User** — every project on your machine.
- **Project** — everyone who clones the repo.
- **Local** — this repo, for you only.

To get the latest changes, run `/plugin marketplace update workflow-skills`, or turn on auto-update for `workflow-skills` under **Marketplaces** in `/plugin`.

## Set up

Add a **DevRel** section to your project's `AGENTS.md` so the commands don't have to ask:

```text
## DevRel

- GitHub handle: your-handle
- Orgs to monitor: your-org, another-org
- Standup posts to: Slack
```

## Commands

| Command                                    | Use it to                                                                                       |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| `/devrel:daily-standup [date] [orgs]`      | Draft your standup from the previous weekday's GitHub activity and your answers, ready to paste |
| `/devrel:community-triage [orgs] [window]` | See open issues and pull requests from people outside your orgs, and where you've been tagged   |

- `daily-standup` reports on the previous weekday (Friday on a Monday) unless you give a date. It asks for your last standup and today's plan, and includes only the work you confirm. Paste an old standup instead, and it tidies that one without checking GitHub.
- `community-triage` looks at the last two months unless you give a window, such as `last 6 months`. It lists bot pull requests apart, so you can merge them in one go.
- The table uses Claude Code plugin names. With a plain install, drop the prefix: `/daily-standup` in Claude Code, `$daily-standup` in Codex. In other agents, ask by name, such as "run community-triage for the last 6 months".

## Contributing

Issues and pull requests are welcome, especially for a command that misreads your activity or has fallen behind GitHub's search. In a pull request:

- Change one skill where you can.
- Update its `evals/evals.json`.
- Keep `SKILL.md` under 200 lines and its description under 550 characters, and give a new skill a name no other set uses.
- Run the checks:

| Script              | Use it to                                                                                                                                     | Needs                       |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| `pnpm format`       | Format everything with Prettier                                                                                                               | `pnpm install` first        |
| `pnpm format:check` | Check formatting without writing                                                                                                              | `pnpm install` first        |
| `pnpm validate`     | Validate the Claude Code marketplace and plugin manifests                                                                                     | the Claude Code CLI on PATH |
| `pnpm check:skills` | Check every skill against the Agent Skills rules and the house limits: 200 lines, a 550-character description, and a name no other skill uses | Node                        |

## Support

If these skills save you time, [buy me a coffee](https://buymeacoffee.com/timonwa).

For building web apps, see [engineering-skills](https://github.com/Timonwa/engineering-skills). For writing docs, blogs and newsletters, see [writing-skills](https://github.com/Timonwa/writing-skills).

## License

[MIT](LICENSE)
