# Context-db Update Usage

The usage folder, `{usage_dir}/`, is for agents working in other projects that
use this one. It holds the bare minimum such an agent needs to know to use
this project successfully. Those projects mount the folder in their own
knowledge base, or list it as global context, so its reader may never have
seen this repository.

Decide first whether there is anything to store. Think about using this
project from outside: where to start, the rules its users must follow, the
mistakes they make. If Folders below says the usage folder does not exist yet,
consider the whole project. Otherwise consider what this session changed or
showed, and the user instruction at the end of this output if there is one.
Would an agent in another project use this one wrongly, or fail to use it,
without it? If not, {nothing_to_add}.

Once the folder exists, most runs change nothing. That is the normal outcome,
not a failure. Every addition dilutes what is already there, and a project
that already tells its users how to use it needs only a few lines here that
say where to look.

## What belongs

What an agent needs in order to use this project, and that the project does
not already tell its users:

- What the project is for, and when to use it.
- Where to start, and where the project describes its own interface.
- Which way in is the right one for which job, when there are several.
- Rules its users must follow that the interface does not enforce.
- Mistakes its users make.

Two kinds of thing stay out.

What the project already tells its users stays where it is: its README, its
docs, the definition of its API, its help text, its examples. Never reprint an
API, a schema, a list of commands or flags, or a configuration reference. Say
where it is, and add only what it leaves out. The rule under Context-db Is Not
a Mirror of the Code, below, holds here for a different reader: one who uses
this project and does not read its insides. So the test for every line is
whether that reader would learn it from what the project shows its users. If
so, leave it out.

Inside knowledge stays out too: why the project is built the way it is, its
own conventions, how to change it, its plans. That is for agents working on
this project. It belongs in the project folder, `{project_dir}/`, which
`/context-db update` writes.

## Where it goes

Write inside the usage folder and nowhere else. If it does not exist yet,
create it, starting with its descriptor, `{usage_descriptor}`. The description
in the descriptor is the one line an agent in another project sees before it
decides whether to look inside, so say there what this project is and what the
notes cover.

When the folder exists, run `{toc_usage_cmd}` to see what is already
documented, and open only the files whose descriptions suggest they cover the
topic. Update an existing file when it covers the topic. Create a file only
for a genuinely new topic. Delete what is no longer true, and what the project
now tells its users itself. A smaller, accurate usage folder beats a larger
one.

The folder is read from wherever another project mounts it, so it has to stand
on its own:

- Link only to files inside the usage folder. To point at anything else in
  this project, give its URL if it is published. Otherwise name the project
  and give the path from the top of its repository, as in "`api/openapi.yaml`
  in the acme-ledger repository".
- Call the project by its name. "This project" and "here" mean something else
  to a reader in another repository.

## Finish

Run:

    {check_cmd}

It checks the format of the project folder and of the usage folder. Fix what
your change caused, and run it again until that is clean. If it reports
problems in files you did not touch, leave them, and mention them in one line
with a suggestion to run `/context-db maintain`.
