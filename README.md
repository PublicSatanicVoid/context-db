# context-db

A set of skills for coding agents. They keep a knowledge base for your project
as Markdown files in your repo, and tell the agent when to read it and when to
add to it.

**Built on the [Open Knowledge Format](https://github.com/GoogleCloudPlatform/open-knowledge-format)
(OKF)**, an open standard for knowledge that agents can read.
[What OKF is, where it came from, and how context-db uses it](https://cart0113.github.io/context-db/okf.html).

Documentation: <https://cart0113.github.io/context-db/>

## Two kinds of knowledge

context-db keeps two kinds of knowledge, because they have two readers.

| | Project knowledge | Usage knowledge |
| --- | --- | --- |
| Who it is for | Agents working on your project | Agents in other projects that use yours |
| What it holds | Decisions and their reasons, conventions, pitfalls, plans | Where to start, the rules for calling your project, the mistakes its users make |
| Where it is kept | The project folder, `<name>-project/`, in `context-db/` | A [usage folder](https://cart0113.github.io/context-db/layout.html#usage-folders), `<name>-usage/`. There can be several. |
| What writes it | `update`, `wip`, and `maintain` | `update --usage` and `maintain --usage` |
| When it is read | First, on every task in your project | In a project that uses yours, when a task there involves your project |

Project knowledge is internal. It drives the work on your project from day to
day, and nobody outside the project needs it. Usage knowledge is external. It
is to agents in other projects what your docs are to people, and it is
optional.

The two work together, because both are folders of short notes in the same
format. A project
[mounts the usage folders of the projects it uses, or finds them with one line of settings](https://cart0113.github.io/context-db/layout.html#how-another-project-reads-it).
From then on every `/context-db prompt` lists them next to its own project
folder, and the agent looks into one the same way it looks into its own notes.
So what another project says about using it is as easy to reach as what your
project knows about itself.

Your own project knowledge still comes first. The agent starts there on every
task, because it applies to everything done in your repository. It looks into
another project's usage folder when the task involves that project, and before
it reads that project's code.

Both are standard OKF. The index of each folder is built on the fly from its
notes, so by default neither kind has `index.md` files to keep in step. You can
[keep `index.md` files as well](https://cart0113.github.io/context-db/layout.html#keeping-index-md-files-anyway),
and context-db works with both.

## Example

Before a task, type the command, then the task on a new line. It needs no
quotes:

```text
/context-db prompt

Users report a bug here:

https://issues.example.com/PAY-482

It looks like it is in the new receipts database code.
Can you investigate and propose a fix?
```

The agent lists the knowledge base, opens the notes on the database schema and the plan
for the receipts work, and skips everything else. Then it finds the cause and
proposes a fix.

When the work is done:

```text
/context-db update --push
```

The agent writes down anything the next agent would need, then commits and
pushes. Most of the time there is nothing to write down, and it says so.

`--push` is optional. So is `--commit`, which commits and does not push. With
neither, the agent leaves the commit to you.

## Benefits

- Your project's knowledge is kept as a hierarchical wiki of short Markdown
  notes in your repo, in the [Open Knowledge Format](https://cart0113.github.io/context-db/okf.html). Every note has a
  one-line description, so the agent finds the few that match the task without
  reading a large instructions file on every turn.
- Two commands bracket the work: `/context-db prompt` before a task and
  `/context-db update` after it. The agent reads and writes the knowledge base
  when you say so, which refreshes its context during long work sessions.
- context-db is nothing more than context: canned instructions plus your own
  rules, sent when you run a command. Your rules are plain Markdown files in
  `context-db/configuration/`, named after the commands: `ON_PROMPT.md` is added
  to every `prompt` and `ON_UPDATE.md` to every `update`.
  [How it all fits together](https://cart0113.github.io/context-db/commands.html#how-it-all-fits-together) shows every word the agent receives.
- A small Python script builds each folder's OKF index
  [on the fly](https://cart0113.github.io/context-db/layout.html#dynamic-indexing), from the notes as they are at that moment. No `index.md`
  files are kept in your repo, so there is nothing to keep in sync and the
  index cannot drift from the notes.
- The knowledge base holds only what the code cannot say. Agents are told to
  watch for notes that repeat the code, because a copy drifts. `update` stores
  only what future agents need to know to be effective, and `maintain` clears
  out what has gone stale, so it stays small and efficient.
- `wip` keeps a short list of the work in progress with a plan for each, so a
  new session can pick up long work where the last one stopped. It is useful on
  a new project, where one feature often takes many agent sessions.
- Shared standards and reference material are mounted as background folders.
  The agent is told which folders are background and which is the project's
  own, and it writes only to the project's. It knows which knowledge is
  critical to the project, and can still find background knowledge when it
  needs it.

## Install

Paste this into your coding agent, in the project where you want it:

```text
Set up context-db in this repository. Follow the Install steps in the README at
https://github.com/cart0113/context-db
```

The agent copies the skills into your project, asks you a few questions, and
creates the knowledge base. These are the steps it follows. You can also run
them yourself. You need Python 3.8 or newer.

1. Copy the skills into the project:

   ```bash
   git clone -b v0.1 https://github.com/cart0113/context-db /tmp/context-db
   mkdir -p .claude/skills
   cp -r /tmp/context-db/skill/context-db .claude/skills/
   ```

2. Set it up. An agent runs this command and follows the instructions it
   prints:

   ```bash
   python3 .claude/skills/context-db/context-db.py configure
   ```

   In Claude Code you can type `/context-db configure` instead. To set it up
   with no agent at all, run the same script with `configure --project <name>`.

[Setup](https://cart0113.github.io/context-db/setup.html) has the full steps.

## What it is

context-db is a set of skills that you install in a coding agent such as Claude
Code. They come as one folder and show up as five commands under `/context-db`.

The commands work on a folder in your repository called `context-db/`. That
folder is the knowledge base. It holds what an agent cannot work out by reading
your code and its comments: your conventions, the decisions you made and why,
the mistakes to avoid, and the plan for the work in progress. It is never a copy
of the code. What the code already says stays in the code.

Everything in it is a Markdown file with a short description at the top. When
the agent looks into a folder, the script lists what is inside, one line each
with its description, built from the files on the spot. The agent reads that
list, opens the one or two files it needs, and leaves the rest alone. Nothing is
generated ahead of time, so the list is never out of date.

There is no database and no server, in spite of the name. It is a folder of text
files and one Python script.

```
your-project/
├── .claude/skills/context-db/      the skills: SKILL.md, context-db.py, prompts/
└── context-db/
    ├── configuration/              settings and rules, all plain Markdown
    │   ├── settings.md             project name, Python command, main branch
    │   ├── ON_PROMPT.md ...        the project's rules for each command
    │   └── ON_PROMPT.local.md ...  your own rules, gitignored (optional)
    ├── acme-payments-project/      the project folder: project knowledge
    │   ├── architecture.md
    │   ├── data-model/
    │   ├── acme-payments-usage/    a usage folder: usage knowledge (optional)
    │   └── wip/                    optional: wip.md lists the work in progress
    ├── coding-standards/           a background folder shared with other projects
    └── acme-ledger-usage -> ...    the usage folder of a project that yours uses
```

## The commands

| Command | What it does |
| --- | --- |
| `/context-db prompt` | Before a task. Looks up what the knowledge base says about it. |
| `/context-db update` | After a task. Writes down what the next agent would need, if anything. `--usage` writes down what other projects need to know to use this one. Optional: `--commit` also commits, and `--push` commits and pushes. |
| `/context-db wip` | Optional, for long work. Keeps a short list of the work in progress. `--list`, `--cleanup`, `--clear`. |
| `/context-db configure` | First, and whenever you like. Sets context-db up by asking a few questions; edit the files by hand afterwards. |
| `/context-db maintain` | Now and then. Removes what the code and the docs already say and what is no longer needed, fixes what has drifted, and splits and reorganizes. `--use-git-diff` also reads the git history for what has gone out of date. `--usage` tidies the usage folders instead. |

`/context-db --help` prints the same list.

Nothing is loaded when a session starts. The agent reads the knowledge base when
you run one of these commands. After `/context-db prompt` it may also add to it
as it works; `/context-db configure` asks whether you want that.

Each command gives the agent a set of instructions, so that you do not have to
type them every time. You add your own rules in a few plain Markdown files in
`context-db/configuration/` and edit them by hand. `ON_PROMPT.md` holds the
project's rules for `prompt`, shared with everyone. `ON_PROMPT.local.md` holds
rules that are only yours, and is gitignored. The other commands have the same
pair. `/context-db configure` is a helper that writes a first version of them
by asking you a few questions.

To tell the agent something, type the command, start a new line, and write it
there. It needs no quotes.

Outside Claude Code, run the same commands from a terminal:

```bash
python3 .claude/skills/context-db/context-db.py prompt "add a refund endpoint"
```

## Motivation

On a large project that runs for months, every agent session starts knowing
nothing. It has to rediscover the conventions, the decisions already made and
why, the mistakes from last time, and where the current work stands.
context-db is an explicit memory for that: a folder of short notes in your
repository that you and the agent keep up as the project goes, and that the
agent reads when you ask it to.

The idea builds on Andrej Karpathy's
[LLM wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f):
have the LLM keep a wiki of what it has learned, instead of working everything
out again each time.
context-db uses that idea to cut down how much context has to be loaded for
each task, which keeps the agent focused and efficient.

The usual answer is a big `AGENTS.md` or `CLAUDE.md`. That file is loaded into
every session in full, whatever the task, and as it grows the problems are well
known. Most of it has nothing to do with the task at hand, and the part that
matters gets lost in the rest. The agent trusts it and reads less of the code.
Nobody notices when it goes out of date, so the agent repeats what it gets
wrong. Rules read at the start of a long session have faded by the time the
work they apply to comes up.

A memory of this kind has a cost that is easy to miss. A note is not free once
it is written. Every later session has to read past it, someone has to keep it
true as the code changes, and when nobody does, it misleads. A note earns its
place only while it prevents more mistakes than it causes, and it is worth
less as time passes: the work it was about gets finished, and the code it
described gets replaced.

An agent does not weigh that cost by itself. It is trained to finish the task
in front of it, and what its work costs later is not part of that task. So it
writes too much. It adds a note for everything it learned, sums up code it has
just read, starts a second note where one already covers the topic, and adds a
paragraph where a correction was needed. It does not delete. A knowledge base
kept that way grows until it is in the way. The long view has to come from
somewhere else, and context-db puts it in the instructions the agent gets each
time it reads or writes.

context-db keeps one rule above all, and repeats it to the agent on every
command: the knowledge base is not a mirror of the code. Anything an agent can
learn by reading the code, its comments, and your docs stays there. A note that
copies it is a second version, and it drifts out of date every time the code
changes, while the next agent goes on trusting it. So the knowledge base keeps
only what the code cannot say: why a decision was made, the conventions and
pitfalls the code does not show, rules that come from outside, and the plan for
the work in progress. `update` follows that rule when it writes. `maintain`
goes looking for notes that break it.

A second rule goes with every command that writes: keep it small. Write the
least that does the job. Keep each fact in one place. Rewrite what has changed,
and do not add to it. Delete what is no longer needed. Ask when it is not clear
whether something is still needed. The agent is told that leaving the knowledge
base smaller is as good a result as leaving it larger.

context-db hands the agent small pieces of text at set points in the work
instead of one big file:

- `prompt`, right before a task: how to list the knowledge base, the plans for
  the work in progress, and your rules. The agent opens only the notes that
  match the task.
- `update`, after a task: whether anything needs to change at all, what belongs
  in the knowledge base and what does not, and which notes the session showed
  to be wrong. Most of the time nothing changes.
- `maintain`, now and then: how to find notes that repeat the code, have
  drifted from it, or are no longer needed, and remove them.
- `wip`, during long work: how to keep a short record of where things stand.

The rest stays out of the agent's context. Where a note and the code disagree,
the agent is told to trust the code and tell you.

Keep it small. If deleting a note would not make the agent do anything wrong,
delete it.

## Documentation

- [Setup](https://cart0113.github.io/context-db/setup.html)
- [Commands](https://cart0113.github.io/context-db/commands.html), with the
  exact text each one gives the agent
- [Layout](https://cart0113.github.io/context-db/layout.html): what goes where
  in the knowledge base, what a file looks like, and how to share knowledge
  between projects
- [The Open Knowledge Format](https://cart0113.github.io/context-db/okf.html):
  what it is and which parts context-db uses

## Working on context-db itself

```bash
python3 -m venv .venv
.venv/bin/pip install pytest pyyaml ruff -r docs/requirements.txt
.venv/bin/python -m pytest tests
.venv/bin/sphinx-build -W docs docs/_build/html
cp hooks/pre-commit .git/hooks/pre-commit
```

The docs are Markdown files in `docs/`, built with Sphinx and the PyData theme.
This repository uses its own skills on its own `context-db/` folder.

## License

MIT
