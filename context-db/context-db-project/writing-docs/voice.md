---
type: Convention
description:
  How the docs and README must read — plain, simple, not AI-sounding, no first
  person, ideas and not studies; the words to use (project knowledge, usage
  knowledge, project folder, background folder); how to show a command in an
  example
---

# Voice

## What the owner asked for

On 2026-11-10 the repository owner said of earlier docs: "I have found them very
AI written, not clear. I just want it clear simple." And: "Really, this is a set
of skills, be clear what it is."

## What that means in practice

This list is an interpretation of that feedback, drawn from what was removed in
the v0.1 rewrite of the docs.

- Say what a thing is in the first sentence, in everyday words. "context-db is a
  set of skills that you install in a coding agent."
- Show a concrete example before explaining an idea: the folder, a file, the
  command the user types.
- Describe commands as steps the agent takes, in a numbered list.
- No slogans and no bold lead-in phrase at the start of each bullet.
- No em dashes in prose. Use a full stop or a comma.
- No "not X but Y" constructions and no lists of three for rhythm.
- No filler words: simply, just, seamlessly, powerful, robust, deliberately.
- Prefer a paragraph or a small table to a page of tiny headed sections.

## Showing a command

The owner types the command on its own line, then a blank line, then the
instruction, and never puts the instruction in quotes: "I always new line, never
quote" (2026-11-11). Every example of a `/context-db` command is written that
way, in the docs, the README, and the prompt files:

    /context-db prompt

    Users report a bug here: ...

Flags stay on the command's line. Only the terminal form keeps quotes
(`context-db.py prompt "..."`), because the shell needs them.

## Person

No "we" or "I". Address the reader as "you". "Copy the skill into your project",
not "We recommend copying the skill."

## Ideas, not studies

The docs argue from ideas and cite no studies. The owner, 2026-11-22: "do not
have any thing about studies. Just keep in general, idea based. No need to
appeal to authority, or if we do briefly." The ideas "should hold together on
their own". The credit to Karpathy and the OKF history stay.

## Words

| Use | Not |
| --- | --- |
| project knowledge | internal knowledge, inside knowledge |
| usage knowledge | external knowledge, API knowledge |
| project folder | project bundle |
| background folder | background bundle, external folder |
| global context, global folder | external source, global bundle |
| a set of skills | a tool, a framework, a system |
| settings | configuration (except for the file name) |
| knowledge base | database, store |

The owner chose "project" and "usage" for the two kinds of knowledge on
2026-11-22, over internal / external and development / usage. They are the
names of the folders, the flag, and the setting, so nothing had to be renamed,
and "external" also reads as knowledge that comes from outside, which is what a
background folder is. "Internal" and "external" may explain the two once, as
the README does.

"Bundle" and "concept" are OKF's words. Use them only on the OKF page and when
explaining how context-db maps onto OKF. The same vocabulary applies to the
prompt files, because the docs include them verbatim.
