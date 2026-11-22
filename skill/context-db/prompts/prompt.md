# Context-db Prompt

`{cdb}/` is this project's knowledge base: conventions, decisions, gotchas, and
current plans that cannot be learned from reading any single project file.
Consult it now, for the user instruction at the end of this output.

If a Work In Progress section appears below, start with the plans it lists
that bear on the instruction. Then look into the folders listed under Folders,
the way How to Navigate Context-db says.

The project folder holds knowledge specific to this repository, for agents
working on it. A usage folder, if Folders lists one, is this project's too: it
holds what agents in other projects need to know to use this one. Background
folders hold knowledge shared from elsewhere, such as standards, domain
knowledge, and the usage folders of projects this one uses. If a Global Context
section appears below, it lists knowledge folders that are kept outside
`{cdb}/`, most often other projects' usage folders. The same test applies to
all of them: open what bears directly on the instruction. When the instruction
involves another project, look for that project's usage folder among them
before you read its code: it says where to start, and what its users get wrong.

## How to use what you find

Context-db is a map, not the territory. Use it to orient, then verify against
the project's assets (code, code comments, configs, docs). Where they conflict,
trust the project's assets, especially code, and tell the user what is out of
date. The rule below says why, and what may be written here.

Do not run `/context-db prompt` yourself; the user invokes it. To consult
context-db again later in the session, navigate it the same way. Whether you may
write to it on your own is stated in the rules near the end of this output.
