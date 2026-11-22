# Context-db Update Usage

A usage folder holds usage knowledge: the bare minimum that an agent working
in another project needs to know to use this one successfully. Those projects
mount the folder, or list it as global context, so its reader may never have
seen this repository.

This project keeps its usage notes here: {usage_list}. The Folders section
below describes each of them, or says that it does not exist yet.

Decide first whether anything needs to change. Think about using this project
from outside: where to start, the rules its users must follow, the mistakes
they make. If there is a user instruction at the end of this output, it says
what to consider, and you look no further. With none, consider what this
session changed or showed, and for a usage folder that does not exist yet, the
whole project. Would an agent in another project use this one wrongly, or fail
to use it, without the change? If not, {nothing_to_add}.

Once a usage folder exists, most runs change nothing. That is the normal
outcome, not a failure. A project that already tells its users how to use it
needs only a few lines here that say where to look.

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
so, leave it out. When something is missing there and would be better said
there, tell the user so in one line, and write the note all the same: it goes
once the project says it.

Project knowledge stays out too: why the project is built the way it is, its
own conventions, how to change it, its plans. That is for agents working on
this project. It belongs in the project folder, `{project_dir}/`, which
`/context-db update` writes. When the session or the user instruction holds
some, say so in one line and suggest that command.

## Where it goes

Write inside a usage folder and nowhere else. When there are several, each is
for different readers: its description says who they are, or its name does
while it does not exist yet. Put a note in the one whose readers need it, and
never the same thing in two. Do not start a usage folder that is not listed.
Adding one is the user's decision, made with the `usage_folders` setting in
`{settings}`.

Create a listed folder that does not exist yet when you have something for it,
starting with its descriptor, which Folders names. The description there is
the one line an agent in another project sees before it decides whether to
look inside, so say what this project is and what the notes cover. The body of
the descriptor is the place to say where the project describes its own
interface.

In a folder that exists, run `{toc_cmd} <folder>` first, to see what is already
documented. Fix what this session made untrue, and delete what the project now
tells its users itself.

A usage folder is read from wherever another project mounts it, so it has to
stand on its own:

- Link only to files inside the same usage folder. To point at anything else
  in this project, give its URL if it is published. Otherwise name the project
  and give the path from the top of its repository, as in "`api/openapi.yaml`
  in the acme-ledger repository".
- Call the project by its name. "This project" and "here" mean something else
  to a reader in another repository.

## Finish

Read your change once more as an agent in another project would, cold, and cut
every line that agent would not miss. Then run:

    {check_cmd}

It checks the format of the project folder and of every usage folder. Fix what
your change caused, and run it again until that is clean. If it reports
problems in files you did not touch, leave them, and mention them in one line
with a suggestion to run `/context-db maintain`.

Tell the user in a line or two what you added, changed, and deleted.
