# Context-db Maintain Usage

Tidy this project's usage folders ({usage_list}), following the user
instruction at the end of this output if there is one. With none, look at all
of them. With a folder or a topic, look only there.

A usage folder holds usage knowledge: the bare minimum that an agent working
in another project needs to know to use this one successfully. Those projects
mount the folder in their own knowledge base, or list it as global context, so
its reader may never have seen this repository.

Your main job is to enforce the rule under Context-db Is Not a Mirror of the
Code, below, for that reader: one who uses this project and does not read its
insides. Every note that repeats what the project already tells its users is a
copy that will drift.

Check first, change second. A usage folder that is in good shape needs
nothing. If you find nothing worth changing, say so in one line and stop. If
Folders below says that no usage folder exists yet, there is nothing to tidy:
say so, suggest `/context-db update --usage`, and stop.

## What to look for

Start with the format check. Run:

    {check_cmd}

It checks the project folder and every usage folder, and names files and
descriptions that are too long, folders with too many items, broken links,
links that leave a usage folder, and missing descriptions. Then run
`{toc_cmd}` on each usage folder in scope, and on its subfolders, and read the
notes there. For this command, every note in scope bears on the task.

First, what the project already tells its users. For every note, open what the
project shows its users about the same thing: its README, its docs, the
definition of its API, its help text, its examples. Compare:

- **Repeats the project.** A reprinted API, a schema, a list of commands or
  flags, a configuration reference, anything the project already tells its
  users: delete it, and say where it is instead. Keep only what that leaves
  out.
- **Project knowledge.** Why the project is built the way it is, its own
  conventions, how to change it, its plans. Someone who uses the project does
  not need it. If the next agent working on this project would, move it to the
  project folder, `{project_dir}/`. Otherwise delete it.
- **Wrong.** Fix what has drifted from the project as it is now, and every
  path or URL that no longer leads anywhere. Delete what is about a part of
  the project that is gone.
- **Does not stand alone.** Wording such as "this project" or "here", which
  means something else to a reader in another repository, becomes the
  project's name. A link that leaves its usage folder becomes a URL, or the
  project's name and the path from the top of its repository.

Then the shape of each folder:

- **Too long.** A file over about 150 lines becomes smaller files, or a
  subfolder of the same name with a descriptor and one file per topic.
- **Several topics in one file.** The sign is a description that needs more
  than a line or two to say what the file holds. Split it, one topic to a
  file.
- **Too many items.** A folder with more than about 10 items gets subfolders
  that group related files.
- **Duplicated.** Two files on one topic become one. So do two notes that say
  the same thing in two usage folders: keep it in the folder whose readers
  need it.
- **Vague descriptions.** A description that does not say what the file holds,
  or no longer matches it, gets rewritten. The one in a usage folder's own
  descriptor matters most: it is all an agent in another project sees before
  deciding whether to look inside.
- **Not worth keeping.** Ask of each note: if it were deleted, would an agent
  in another project use this one wrongly, or fail to use it? If not, it goes.

## How to change it

- Delete a note without asking only when it is plainly false or plainly
  repeats the project. For any other note you want to delete, list it and ask
  the user first. Cutting a note down is not deleting it.
- When you split, move, or rename a file, search its usage folder for links to
  it and fix them.
- Change nothing outside the usage folders, except to move project knowledge
  into the project folder.

## Finish

Run:

    {check_cmd}

and fix what it reports in the usage folders, until that is clean. If it
reports problems elsewhere, leave them, and mention them in one line with a
suggestion to run `/context-db maintain`.
Then tell the user in a few lines what you removed because the project already
says it, and what you moved, fixed, split, or merged.
Leave the changes uncommitted unless the user asks you to commit them.
