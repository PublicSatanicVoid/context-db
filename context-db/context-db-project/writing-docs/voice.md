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

On 2026-11-23, of a section that opened the home page by explaining the two
kinds of knowledge with a five-row comparison table and four paragraphs: "too
detailed, the table was weird. Too explicit. We can be more simple." And, when
the agent set about cutting it to a stub: "the info you had was good, it was
just too detailed and too soon in the page."

The same day, of a Motivation section that opened with what goes wrong on a
large project and ran to ten paragraphs: "less vacuum salesman throwing dirt
on the carpet and more about just what it is."

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
- On the home page and the README, give an idea a few plain sentences. Keep
  the substance, cut the detail, and link to the page that has it. Do not lay
  out every property of a thing in a table.
- Say what context-db is and does. Do not build up a problem first in order
  to sell the answer to it.
- Do not repeat a noun through a sentence or a short paragraph. The owner
  asked for one "without the word project used so often".

A correction to one passage applies to the whole page. On 2026-11-23, after
pointing at three passages one at a time, the owner said: "I want you to fix
everything you find to make it complete." Look for the same fault in the other
sections and fix it in the same pass.

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
names of the folders and the setting, so nothing had to be renamed,
and "external" also reads as knowledge that comes from outside, which is what a
background folder is. "Internal" and "external" may explain the two once, as
the README does.

The lead sentence of the home page and the README is the one exception: it
says "usage information: the knowledge". The owner chose that on 2026-11-23
over the agent's "usage knowledge: the information". Leave it.

"Bundle" and "concept" are OKF's words. Use them only on the OKF page and when
explaining how context-db maps onto OKF. The same vocabulary applies to the
prompt files, because the docs include them verbatim.
