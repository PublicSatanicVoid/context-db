---
type: Decision
description:
  Why each folder's index is built on demand by `toc` and no index.md is kept
  by default, when an index.md is read or only checked, and why the owner kept
  this over index files built by a commit hook (2026-11-11, 11-19, 11-22)
---

# Dynamic indexing

`toc <folder>` reads the frontmatter of a folder's files and subfolders and
prints the listing in OKF's `index.md` layout. Nothing is written. The agent
runs it every time it looks into a folder, and again on a subfolder whose
description matches. `toc --check` is the format check, run after writes, by
the pre-commit hook, and in CI.

OKF lets a folder carry an `index.md` and only constrains its layout if one
exists, so building it on demand is conformant. Section 8 of the spec says so
outright: "consumers MAY synthesize one on the fly when none is present". The
docs present it as a feature: this is how context-db implements OKF's index.

## History

- v0.0 printed a TOC on demand with a script, after committed `-toc.md` files
  broke on per-user symlinked folders.
- v0.1 briefly committed a generated `index.md` per folder, for file-read
  navigation and GitHub browsing. That needed a regenerate step after every
  write, a CI drift check, a rule for merge conflicts, a gitignore filter so
  private notes stayed out, and owning repositories generating indexes for
  shared folders.
- On 2026-11-11 the owner reversed it: "I liked the way I was doing it before",
  "Before this v0.1 work, that was a major part of the system." The v0.0 way
  "was working well".

## A folder that comes with an index.md

The owner, 2026-11-19: "the index.md idea is so we can work with standard
version compliant okf folders. if it's there, we use it and do not dynamically
generate the toc." And: "The index.md is optional tho - we work with both
formats". So for a background folder or a
[global folder](./global-context.md), `toc` prints the folder's own `index.md`
when it has one and builds the listing when it has none, folder by folder.

The folders the commands write, the project folder and the usage folders, are
the exception: `toc` never reads an `index.md` there, because a listing built
from the files cannot be stale. Until 2026-11-22 one there was an error. The
owner then asked for standard OKF to be "first class", for someone who "might
decide to have a commit hook that builds index.md files", and narrowed it to
"Just we need to accept index.md files". So the check accepts one and warns
when it does not match its folder. The listing says when a folder keeps one,
because the agent cannot keep in step a file it does not know is there.
context-db builds none itself.

Two details the owner has not ruled on. An `index.md` with no entries falls
back to the built listing. A folder with an `index.md` and no descriptor is
described in `prompt` by the titles its index lists, because OKF gives a folder
no description of its own.

## Index files built by a commit hook: considered, rejected

On 2026-11-22 the owner asked whether `index.md` should become the folder
file, built by a commit hook, with "no more toc script at prompt time", so
that the project would look less bespoke. After the answer below the owner
kept things as they are: "this is a standard format".

- Building the index on the fly is itself standard (above), and a reader may
  never reject a folder for having no `index.md`.
- A hook runs only at commit, and only in a clone that installed it, so the
  agent would read a stale index in between. `toc` could not go away either:
  mounted folders and notes not yet committed still need it.
- A committed listing is a second copy of every description, which is what
  2026-11-11 removed.
- `index.md` cannot replace the descriptor. OKF gives a subfolder's index no
  frontmatter, so it has nowhere to put the folder's description.

## The navigation instruction is core text

The owner: "this is just something fundamental in the core instructions given
to the agent on every skill invocation." It lives in one file,
`skill/context-db/prompts/navigate.md` (v0.0 called it Read Mechanics), and
`prompt`, `update`, `maintain`, `wip`, and `wip --maintain` all include it.
`SKILL.md` repeats it. `prompt` builds no listing itself; it only tells the
agent how to call the script. A test fails if a reading command leaves it out.

## Costs accepted

- Each folder costs the agent one script call instead of a file read.
- GitHub and Obsidian show folders without the descriptions.

## Flat, not grouped by type

OKF's reference implementation groups index entries under a heading per `type`.
context-db prints two fixed headings, `# Subfolders` and `# Files`. Folders hold
5–10 items, so type headings would add lines without helping the agent choose;
the description does the routing.
