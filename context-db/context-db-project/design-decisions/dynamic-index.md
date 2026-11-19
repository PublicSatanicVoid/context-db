---
type: Decision
description:
  Why the project folder has no index.md files — context-db builds each folder's
  OKF index on demand with the hidden `toc` helper, the way v0.0's TOC script
  did, and the agent is told how on every command that reads the knowledge base.
  Reverses v0.1's committed, generated indexes (owner decision, 2026-11-11).
  When a folder's own index.md is used instead, for standard OKF folders that
  context-db does not own (owner decision, 2026-11-19). Also why the listing is
  flat Subfolders/Files and not grouped by type.
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

The project folder is the exception. That part is the implementing agent's
choice, following the 2026-11-11 decision above: context-db writes that folder,
so an `index.md` in it can only be a stale leftover. `toc` never reads one
there, and `toc --check` reports it. The owner was told and let it stand.

Two details the owner has not ruled on. An `index.md` with no entries falls
back to the built listing. A folder with an `index.md` and no descriptor is
described in `prompt` by the titles its index lists, because OKF gives a folder
no description of its own.

## The navigation instruction is core text

The owner: "this is just something fundamental in the core instructions given
to the agent on every skill invocation." It lives in one file,
`skill/context-db/prompts/navigate.md` (v0.0 called it Read Mechanics), and
`prompt`, `update`, `maintain`, `wip`, and `wip --cleanup` all include it.
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
