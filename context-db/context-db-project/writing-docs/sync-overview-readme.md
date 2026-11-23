---
type: Convention
description:
  README and docs/index.md tell the same story and are updated together; the
  agent-facing overview.md is small, independent, and never a copy of either.
---

# README, docs home page, agent overview

| File                                       | Audience         | Sync?                |
| ------------------------------------------ | ---------------- | -------------------- |
| `README.md`                                | Humans on GitHub | yes                  |
| `docs/index.md`                            | Docs site        | yes                  |
| `context-db/<project>-project/overview.md` | Agents           | no, and 20–40 lines  |

The README and the docs home page share their opening, "Example", "Two kinds
of knowledge", "Benefits", "Install", "What it is", the commands, and
"Motivation" almost word for word.
Only the links differ: full site URLs in the README, relative ones on the home
page. The
command list is the `--help` summaries verbatim, which a test enforces. When
one changes, change the other. The home page uses tabs where the README uses a
tree. The README's Install section also
carries the steps themselves, because the install prompt sends agents there.

[overview.md](../overview.md) is not a copy of the README. It is what a new
contributor would be told in 30 seconds before touching the code: API surfaces,
what is generated versus hand-edited, what to run after a change. If a section
reads like "what this project is", it is in the wrong file.

The three are separate files, never symlinks: the agent overview needs
frontmatter, and the README must not have it.
