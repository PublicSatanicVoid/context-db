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
- There is no switch. Patterns that are set are listed on every `prompt`. The
  owner first asked for a `use_global_context` setting with a flag to match,
  and removed both on 2026-11-23 with the other flags that narrow a command.
  See [command-set.md](./command-set.md).
- A matched folder is described by the file named after it, taken literally:
  `ledger-usage.okf/ledger-usage.okf.md`. The owner was asked whether the
  `.okf` ending should be dropped and said no.

## The implementing agent's choices

The owner saw the first two in the summary of the work and let them stand. The
last two were not pointed out.

- One optional key in `settings.md`, not a new file. It passes the test in
  [configuration-folder.md](./configuration-folder.md): the script cannot work
  it out.
- A match that `context-db/` already holds is dropped, so
  `../*/context-db/*-project` does not list this project twice. So is each of
  the project's own usage folders, which `prompt` lists under Folders.
- Patterns that match nothing add no section, the way an empty wip list adds
  none.
- The words are "global context" for the feature and "global folder" for one
  matched folder.
