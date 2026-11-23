---
type: Decision
description:
  The five user commands and their order, and why — no flag narrows prompt,
  update, or maintain, because a command is only a starting point; maintain
  apart from update; configure, not init; --show-context, not --dry-run; one
  source for the summaries and the API block. Owner decisions, November 2026.
---

# The command set

The owner fixed the set and the order on 2026-11-11: `prompt`, `update`, `wip`,
`configure`, `maintain`. Use that order everywhere a list of commands appears.

## No flag narrows a command

The owner, 2026-11-23: "I do not want all these switches. By default, prompt,
update, maintain do everything and touch project (including wip) and usage",
and "if you just want to focus on one or the other, just talk to the agent."
context-db is "just a starting point", the common defaults that open a
conversation, and the user shapes the rest in words. The owner wants the docs
to say so: under the API block on the front page, and on the commands page.

- Do not add a flag that narrows what a command looks at or changes how it
  works. `--wip`, `--usage`, `--use-git-diff`, and `--use-global-context` were
  all built and then removed. A flag stays only when it does something a
  sentence should not: `--commit` and `--push`, and the three modes of `wip`.
- `update` goes by what the agent remembers of the session and reads no git.
  It also keeps the plan that the session worked from current, and must be
  very brief about it.
- `maintain` always gets the git history, and the state of git when there are
  plans. The owner: for `maintain`, "it's assumed to use version control".
- `wip --list`, `--maintain`, and `--clear` are the owner's. `--maintain` was
  `--cleanup`: the sweep of every plan, judged by version control. Plain
  `maintain` makes the same check as part of its sweep.
- Narrowing in words does not shorten the message. The script cannot read the
  instruction, so the agent skips the sections that are out of scope.

Before changing the API again, show the owner the whole of it as typed, as the
`API` block, and wait. A full build of scope flags on every command was thrown
away the day it was made.

## maintain is a command again

v0.1 had dropped it in favour of `update "audit <folder> and cut"`. The owner
restored it. Mixing "write down this session's lesson" with "clean up the
knowledge base" made `update` do work when there was nothing to do. So:

- `update` changes only the files its lesson belongs in, leaves format problems
  in other files alone, and stops in one line when there is nothing to change.
  Since 2026-11-22 it also fixes or deletes the notes that the session itself
  showed to be wrong or not needed, and names any others it noticed and asks.
  An agent that a note has just misled is the one that knows the note is wrong.
- `maintain` does sweeps, checks first, and stops when nothing needs changing.
  Its main job is enforcing the not-a-mirror rule (below), and its second the
  keep-small rule.

`configure` asks how freely `update` cleans up. That is the implementing
agent's choice: the owner said only that asking the user how far to go is fine
and "could be a config option". The question writes a sentence into
`ON_UPDATE.md` for an answer other than the default, so the default costs
nothing on each run.

## configure, not init

The owner: "init and configure are the same thing". `configure` with no flags
starts the conversation; with `--project` or any other setting flag it writes
the files and asks nothing. There is no `help` sub-command; `--help` and a bare
call print the list. `toc` is left out of `--help` because only the agent and
CI run it.

## --show-context, not --dry-run

The owner (2026-11-19) wanted "a --dry-run" on every command and rejected the
name in the same sentence: "all this does is invoke the skill and show what
context will be sent to the agent". Nothing is simulated, so the flag is named
for what it does. `--show-context` was the implementing agent's proposal, and
the owner kept it.

The message between the markers must stay byte for byte what the command sends
without the flag. The flag is refused together with `configure`'s setting
flags, because showing must never write.

## One source for the summaries and the API block

`COMMAND_SUMMARIES` in the script is what `--help` shows, and the README table
and the docs home page cards repeat it word for word. A test compares all three
and the section headings of `docs/commands.md`. Change the summary in the
script, then copy it to both pages.

`API` in the script is everything the user types, in one block. The owner
asked for "a code block ... which shows the whole api on the front page".
`--help` prints it, both front pages repeat it, and a test compares them.

## Shared core text

Two prompt files go to the agent on every command that reads or writes notes,
so the system says one thing everywhere: `not-a-mirror.md` (context-db never
restates what the code and its comments say) and `navigate.md` (see
[dynamic-index.md](./dynamic-index.md)). The owner asked for the not-a-mirror
rule to be stressed uniformly "throughout and in our main page, the motivation
section". Edit the rule in that file, and keep the docs' wording of it in step.

A third, `keep-small.md`, goes with every command that writes. The owner asked
for it on 2026-11-22: agents "are too verbose", they duplicate and "write too
much for the problem at hand", so `update` and `wip` need "concise
instructions" that the agent is also keeping the knowledge base minimal, and
"it's ok for agents to ask for guidance on this". The owner's reason: an agent
is trained on the task in front of it and does not weigh what a note costs
later, so the long view has to come from the instructions. The wording of the
rule, the warning for a description over 300 characters, and the first-line
"Delete this once ..." sentence are the implementing agent's choices.
