# workflow-skills

Claude skills for the everyday work around the code and the writing, starting with your standup and community triage.

[![License: MIT](https://img.shields.io/github/license/Timonwa/workflow-skills)](LICENSE)
[![Claude Code plugins](https://img.shields.io/badge/Claude%20Code-plugins-D97757)](#install)
[![GitHub stars](https://img.shields.io/github/stars/Timonwa/workflow-skills?style=flat)](https://github.com/Timonwa/workflow-skills/stargazers)
[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20me%20a%20coffee-support-FFDD00?logo=buymeacoffee&logoColor=black)](https://buymeacoffee.com/timonwa)

## Contents

- [The plugins](#the-plugins)
- [How the skills work](#how-the-skills-work)
- [Install](#install)
- [Set up](#set-up)
- [Commands](#commands)
- [Contributing](#contributing)
- [Support](#support)

## The plugins

Skills are grouped by the tool they work with.

| Plugin   | For                 | Install it if you                                                                |
| -------- | ------------------- | -------------------------------------------------------------------------------- |
| `github` | Your work on GitHub | Post a daily standup, or look after issues and pull requests from your community |

## How the skills work

- Commands run only when you call them.
- They read from GitHub through its command-line tool (`gh`) and report in the chat. They never comment, merge, close or post anything.
- Your GitHub handle and the orgs to watch come from the command's arguments or your project's `AGENTS.md`. Without either, the command asks once.
- Nothing is reported that GitHub didn't return, and nothing goes in your standup that you didn't confirm.

## Install

The commands call GitHub from the shell, so they run in Claude Code, not the Claude app.

1. Install GitHub's command-line tool and sign in:

   ```shell
   gh auth login
   ```

2. Add the marketplace and the plugin in Claude Code:

   ```shell
   /plugin marketplace add Timonwa/workflow-skills
   /plugin install github@workflow-skills
   ```

When it asks for a scope, pick one:

- **User** — every project on your machine.
- **Project** — everyone who clones the repo.
- **Local** — this repo, for you only.

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
| `/github:daily-standup [date] [orgs]`      | Draft your standup from the previous weekday's GitHub activity and your answers, ready to paste |
| `/github:community-triage [orgs] [window]` | See open issues and pull requests from people outside your orgs, and where you've been tagged   |

- `daily-standup` reports on the previous weekday (Friday on a Monday) unless you give a date. It asks for your last standup and today's plan, and includes only the work you confirm. Paste an old standup instead, and it tidies that one without checking GitHub.
- `community-triage` looks at the last two months unless you give a window, such as `last 6 months`. It lists bot pull requests apart, so you can merge them in one go.

## Contributing

Issues and pull requests are welcome, especially for a command that misreads your activity or has fallen behind GitHub's search. In a pull request:

- Change one skill where you can.
- Update its `evals/evals.json`.
- Keep `SKILL.md` under 200 lines and its description under 550 characters.
- Run the checks:

| Script              | Use it to                                                                | Needs                       |
| ------------------- | ------------------------------------------------------------------------ | --------------------------- |
| `pnpm format`       | Format everything with Prettier                                          | `pnpm install` first        |
| `pnpm format:check` | Check formatting without writing                                         | `pnpm install` first        |
| `pnpm validate`     | Validate the marketplace and plugin manifests                            | the Claude Code CLI on PATH |
| `pnpm check:skills` | Fail on a `SKILL.md` over 200 lines or a description over 550 characters | Node                        |

## Support

If these skills save you time, [buy me a coffee](https://buymeacoffee.com/timonwa).

For building web apps, see [engineering-skills](https://github.com/Timonwa/engineering-skills). For writing docs, blogs and newsletters, see [writing-skills](https://github.com/Timonwa/writing-skills).

## License

[MIT](LICENSE)
