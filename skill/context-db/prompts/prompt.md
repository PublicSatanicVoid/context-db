# Context-db Prompt

`{cdb}/` is this project's knowledge base: conventions, decisions, gotchas, and
current plans that cannot be learned from reading any single project file.
Consult it now, for the user instruction at the end of this output.

If a Work In Progress section appears below, start with the plans it lists
that bear on the instruction. Then look into the folders listed under Folders,
the way How to Navigate Context-db says.

The folders hold two kinds of knowledge, in one format, and you read both the
same way.

- Project knowledge is this project's own, for agents working on it. It is in
  the project folder, and it comes first: start there on every task, because
  it applies to everything done in this repository.
- Usage knowledge is what a project tells agents in other projects about using
  it. When the instruction involves a project that this one uses, look for
  that project's usage folder among the background folders and under Global
  Context, and look into it before you read that project's code: it says what
  its users get wrong. This project's own usage folder, if Folders lists one,
  is what it tells others. Look into it when the instruction changes how this
  project is used.

A background folder is any other folder in `{cdb}/`, such as shared standards
or domain knowledge. Global Context, when that section appears below, lists
knowledge folders that are kept outside `{cdb}/`. One test applies to every
folder: open what bears directly on the instruction.

## How to use what you find

Context-db is a map, not the territory. Use it to orient, then verify against
the project's assets (code, code comments, configs, docs). Where they conflict,
trust the project's assets, especially code, and tell the user what is out of
date. The rule below says why, and what may be written here.

Do not run `/context-db prompt` yourself; the user invokes it. To consult
context-db again later in the session, navigate it the same way. Whether you may
write to it on your own is stated in the rules near the end of this output.
