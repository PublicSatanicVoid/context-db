---
type: Decision
description:
  Global context, the third source of knowledge after the project folder and
  background folders — folders that stay in other repositories and are found by
  glob patterns in settings (global_context, use_global_context). Why prompt is
  the only command that lists them, how a matched folder is described, and
  which parts the owner decided on 2026-11-19. Also called global folders,
  external sources, okc usage folders.
---

# Global context

The owner's design (2026-11-19). Knowledge has three sources: the project
folder, which is "privileged"; every other folder in `context-db/`, "real or
symlink", which "is assumed to be okf knowledge"; and folders that stay in other
repositories, found by a glob in the settings.

## What the owner decided

- The patterns live in the settings file and are read "*from* the context-db
  repo": from the repository root, not from the caller's cwd. The pattern the
  owner expects to be common is `../*/okc/*-usage.okf`.
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
  `../*/context-db/*-project` does not list this project twice. Nothing else is
  dropped, so `../*/okc/*-usage.okf` also matches this repository's own `okc/`.
- Without the flag, patterns that match nothing add no section, the way an
  empty wip list adds none. With the flag, the section says that there is none.
- The words are "global context" for the feature and "global folder" for one
  matched folder.

## Not settled

- Nothing in this repository says what `okc` is. The docs explain the owner's
  pattern as a glob and stop there, and the example project does not use global
  context. Ask the owner before describing `okc` anywhere.
