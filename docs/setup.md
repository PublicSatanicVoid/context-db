# Setup

You need Python 3.8 or newer, and a coding agent that can run shell commands.
These steps use Claude Code.

## Ask your agent to do it

Open your project in your agent and paste this:

```text
Set up context-db in this repository. Follow the Install steps in the README at
https://github.com/cart0113/context-db
```

The agent copies the skills into your project, asks you a few questions as a
menu, and creates the knowledge base. That covers steps 1, 2, and 4 below. Read
on to do them by hand, or to see what the agent did.

## 1. Copy the skills into your project

```bash
git clone -b v0.1 https://github.com/cart0113/context-db /tmp/context-db
mkdir -p .claude/skills
cp -r /tmp/context-db/skill/context-db .claude/skills/
```

The skills come as one folder: a Python script, a few instruction files, and
some starter templates. Commit it with your project so that everyone on the team
has the same version.

If you use a different agent, put the folder wherever that agent keeps its
skills. You can also run any command yourself from a terminal:

```bash
python3 .claude/skills/context-db/context-db.py --help
```

## 2. Set it up

In Claude Code, type:

```text
/context-db configure
```

This is the first thing to run. The agent asks for the project name and creates
the folders. Then it asks a few questions as a menu about how it should treat
the knowledge base: whether breaking changes are fine in this project, whether
to read the knowledge base only when you run a command, whether to update it as
it works, and when to split files that grow too long. [Commands](commands.md)
lists them all.

To set it up with no questions:

```bash
python3 .claude/skills/context-db/context-db.py configure --project acme-payments
```

Either way you end up with this:

```text
context-db/
├── configuration/
│   ├── settings.md
│   ├── ON_PROMPT.md
│   ├── ON_UPDATE.md
│   ├── ON_WIP.md
│   ├── ON_CONFIGURE.md
│   └── ON_MAINTAIN.md
└── acme-payments-project/
    ├── acme-payments-project.md
    └── wip/
        └── wip.md
```

Running it again is safe. It never overwrites a file that already exists.

## 3. Make it behave the way you want

Five files in `context-db/configuration/` control how the agent behaves:
`ON_PROMPT.md`, `ON_UPDATE.md`, `ON_WIP.md`, `ON_MAINTAIN.md`, and
`ON_CONFIGURE.md`. Whatever a file says is added to the agent's instructions
every time that command runs.

Open them and edit them by hand. They are plain Markdown, and the agent reads
exactly what they say. `/context-db configure` is a helper that wrote the first
version; run it again if you would rather answer questions than edit.

Those five hold the project's rules, and everyone on the project gets them.
Rules that are only yours go in a file of the same name ending in `.local.md`,
such as `ON_PROMPT.local.md`. It is added after the project's file, and it is
gitignored.

[Commands](commands.md#the-rule-files-control-how-the-agent-behaves) has
examples of rules.

## 4. Tell the agent to leave it alone

Add the text in `.claude/skills/context-db/starters/AGENTS.md` to your
`AGENTS.md` or `CLAUDE.md`.

It tells the agent that the knowledge base exists, and that it should not read
it unless you run a command. `configure` offers to add it for you. This
matters. An agent that loads the whole knowledge base at the start of every
session has less attention left for your task.

## 5. Use it

Before a task, type the command, then the task on a new line. It needs no
quotes:

```text
/context-db prompt

Add an endpoint for refunds. Partial refunds can wait.
```

After it:

```text
/context-db update
```

That is the whole loop: `prompt`, work for as many turns as it takes,
`update`. If you like, `update` can also
[commit and push](commands.md#context-db-update) what the session changed.
For work that runs over several sessions, you can also keep a plan with
`/context-db wip`; it is optional. `prompt` then starts the next session on
that work from the plan, and `update` keeps it up to date. Run
`/context-db maintain` rarely, as a spring cleaning, to cut the knowledge base
back to what is still needed. [Commands](commands.md) explains all five.

Each command is a starting point. It covers the whole knowledge base, and
there are no flags to narrow it. When you want something narrower or
different, say so in plain words after the command.
[A command is a starting point](commands.md#a-command-is-a-starting-point)
has examples.

That loop keeps your project knowledge, which is for agents working on your
project. If other projects use yours, tell `update` to start a
[usage folder](layout.md#usage-folders). It holds your usage knowledge: the
few things their agents need in order to use your project. From then on
`update` and `maintain` look after it as well. To read the usage folder of a
project that yours uses, see
[How another project reads it](layout.md#how-another-project-reads-it).

## Settings

Settings live in `context-db/configuration/settings.md`, which is committed, so
the whole team shares it. They are the `key: value` lines at the top:

```markdown
---
project: acme-payments
python: python3
main_branch: main
---
```

| Setting | Meaning |
| --- | --- |
| `project` | The project's name. The project folder is `context-db/<project>-project/`. |
| `python` | The command the agent uses to run the script. |
| `main_branch` | The branch that `wip --maintain` and `maintain` check the plans in `wip/` against. |

Two more settings are optional.

| Setting | Meaning |
| --- | --- |
| `usage_folders` | Where your [usage folders](layout.md#usage-folders) are kept, as paths from the top of your repository, such as `okf/acme-payments-usage`. `{project}` in a path stands for the project name, and several paths are separated by spaces. Left out, there is one: `<project>-usage/` inside the project folder. |
| `global_context` | Glob patterns that match knowledge folders outside `context-db/`, such as `../*/okf/*-usage`. They are read from the top of your repository, and several are separated by spaces. `prompt` lists the folders they match. [Global context](layout.md#global-context) explains them. |

Edit them by hand. Anything below the `---` lines is yours for notes.

`context-db/configuration/settings.local.md` is yours alone. It is gitignored,
like every `*.local.md` file in that folder, and anything in it overrides the
shared file. Use it when your machine needs
something different, such as a Python that lives in an unusual place:

```bash
python3 .claude/skills/context-db/context-db.py configure --local python=/opt/python3.12/bin/python3
```

### Settings from other files

A settings file can name more settings files. They are plain files on disk that
you write yourself, and they can live anywhere: in a repository your team
shares, or in your home folder. Add a `settings_files` line by hand:

```markdown
---
project: acme-payments
python: python3
main_branch: main
settings_files: ../standards/context-db-settings.md
---
```

Each file on that line is read after the file that names it, and whatever it
sets overrides what was read before. It looks like `settings.md`: Markdown, with
`key: value` lines at the top. Several are separated by spaces. A path is read
from the top of your repository, and it can also start with `~` or `/`.

This one is shared by a team that keeps every project's usage folder in `okf/`,
and finds the others there:

```markdown
---
usage_folders: okf/{project}-usage
global_context: okf/*-usage ../*/okf/*-usage
---
```

With that file, each project writes its own usage notes to `okf/<name>-usage/`,
and reads the usage folders of the repositories checked out next to it.

The files are read in this order. A later one overrides an earlier one, setting
by setting:

1. `settings.md`
2. the files that `settings.md` names
3. `settings.local.md`
4. the files that `settings.local.md` names

So name a file that everyone on the project has in `settings.md`, and a file
that only you have in `settings.local.md`. Your own settings still win over the
team's.

No command creates or changes these files, and no flag sets the
`settings_files` line. If a file on that line is missing or has no `---` block,
the commands stop and say which file it is. They also stop on a line that is
not a setting, in any settings file, so that a misspelt name is not ignored
without a word. `/context-db configure` still runs, and lists every settings
file in the order it is read.

Keep `python` in `settings.md` or `settings.local.md`. The agent reads that one
line itself, from those two files, before it can run the script.

## Check it in CI

This command changes nothing. It exits with an error if a file breaks the
[format](layout.md):

```bash
python3 .claude/skills/context-db/context-db.py toc --check
```

Add it to a pre-commit hook or a CI job.

## See a complete example

The repository has a small, working project in
[`example/`](https://github.com/cart0113/context-db/tree/v0.1/example).
