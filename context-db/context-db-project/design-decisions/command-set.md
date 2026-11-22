---
type: Decision
description:
  The five user commands and their order, and why — maintain apart from update,
  prompt --wip and no update --wip, configure in place of init, --show-context
  and not --dry-run, and one source for the one-line summaries. Owner
  decisions of November 2026.
---

# The command set

The owner fixed the set and the order on 2026-11-11: `prompt`, `update`, `wip`,
`configure`, `maintain`. Use that order everywhere a list of commands appears.

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
  keep-small rule. `--use-git-diff` adds each note's age against the commits
  made to the project since.

## prompt --wip, and no update --wip

The owner asked for both on 2026-11-22 and dropped the second the same day:
keeping a plan current is something plain `update` does when the session
worked from that plan, and `update` must be very brief about it. The split is
one of scope:

- `update` brings the plan the session worked from up to date, from what the
  agent remembers of the session, such as a ticket that was closed.
- `wip --cleanup` is the aggressive sweep of every plan, judged by version
  control.

Do not add `update --wip`, and do not fold `--cleanup` into `update`.

Two parts are the implementing agent's choices. `prompt --wip` with no task
reports where the work stands and waits. And `configure` asks how freely
`update` cleans up: the owner said only that asking the user how far to go is
fine and "could be a config option". The question writes a sentence into
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

## One source for the one-line summaries

`COMMAND_SUMMARIES` in the script is what `--help` shows, and the README table
and the docs home page cards repeat it word for word. A test compares all three
and the section headings of `docs/commands.md`. Change the summary in the
script, then copy it to both pages.

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
