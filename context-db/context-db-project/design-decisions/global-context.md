---
type: Decision
description:
  Global context, the third source of knowledge — folders that stay in other
  repositories, most often their usage folders, found by glob patterns in
  settings. Why only prompt lists them, and which parts the owner decided.
  Also called global folders.
---

# Global context

The owner's design (2026-11-19). Knowledge has three sources: the project
folder, which is "privileged"; every other folder in `context-db/`, "real or
symlink", which "is assumed to be okf knowledge"; and folders that stay in other
repositories, found by a glob in the settings.

## What the owner decided

- The patterns live in the settings file and are read "*from* the context-db
  repo": from the repository root, not from the caller's cwd. The docs and the
  example use the layout the owner described on 2026-11-20, usage folders kept
  in `okf/`: `okf/*-usage` and `../*/okf/*-usage`.
- Only `prompt` sends the list ("probably just on on-prompt").
- A setting says whether every `prompt` sends it. When it is false, only
  `prompt --use-global-context` does.
- A matched folder is described by the file named after it, taken literally:
  `ledger-usage.okf/ledger-usage.okf.md`. The owner was asked whether the
  `.okf` ending should be dropped and said no.

## The implementing agent's choices

The owner saw the first two in the summary of the work and let them stand. The
last two were not pointed out.

- Two keys in `settings.md`, not a new file. Both pass the test in
  [configuration-folder.md](./configuration-folder.md): the script cannot work
  either out. Both are optional. The switch counts as true when it is left out,
  because someone who adds a pattern expects to see its folders.
- A match that `context-db/` already holds is dropped, so
  `../*/context-db/*-project` does not list this project twice. So is each of
  the project's own usage folders, which `prompt` lists under Folders.
- Without the flag, patterns that match nothing add no section, the way an
  empty wip list adds none. With the flag, the section says that there is none.
- The words are "global context" for the feature and "global folder" for one
  matched folder.
