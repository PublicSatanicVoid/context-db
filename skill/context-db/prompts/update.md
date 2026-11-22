# Context-db Update

Decide first whether the knowledge base needs to change at all. Think back
over this session, for two things:

- What you learned that the next agent would get wrong, or miss, without it:
  corrections the user made, conventions, pitfalls, decisions and the reasons
  for them.
- What the notes you read turned out to be: one that is out of date, one that
  sent you the wrong way, one that says only what the code shows.

If there is neither, {nothing_to_add}.

Most sessions change nothing. That is the normal outcome, not a failure.

When there is something, change only what it needs: the one or two files the
lesson belongs in, and the notes that turned out wrong or not needed, which
you fix or delete. Do not tidy, reword, or reorganize anything else on the
way; that is what `/context-db maintain` is for. If you came across other
notes that look out of date, repeated, or no longer needed, name them in a
line and ask the user whether to clean them up.

## What belongs

The rule under Context-db Is Not a Mirror of the Code, below, decides.

A rule that the code does not follow yet still belongs. Say in the entry that
the code does not enforce it yet, so that the next agent does not take the code
as proof that the entry is wrong.

When you know that a note will stop mattering, say when in its first line, as
in "Delete this once the v1 endpoints are gone."

## Where it goes

Write inside the project folder, `{project_dir}/`. The folders listed under
Folders below as background folders are owned elsewhere: never edit one.

Run `{toc_cmd} {project_dir}` first, to see what is already documented.

Some things have a home of their own, and do not go in the main tree:

- Plans and the status of ongoing work: `{wip_dir}/`, which `/context-db wip`
  manages, if the project records them.
- What agents in other projects need to know to use this one: a usage folder
  ({usage_list}), which `/context-db update --usage` writes. Say so in one
  line and suggest that command.
- What must be seen on every run: an ON file in `{conf_dir}/`, the one place
  outside the project folder that you may write to. Each line there costs
  tokens on every run of its command, so ask the user first.

If you learned something that anyone using another project would need, it
belongs in that project's own usage folder as well. Tell the user in one line
what that folder should say.

Context-db is the project's memory. Do not also save this to an auto-memory or
any vendor-specific memory file.

## Finish

Read your change once more as the next agent would, cold, and cut every line
that agent would not miss. Then run:

    {check_cmd}

It checks the format of the whole project folder. Fix what your change caused,
and run it again until that is clean. If it reports problems in files you did
not touch, leave them, and mention them in one line with a suggestion to run
`/context-db maintain`.

Tell the user in a line or two what you added, changed, and deleted.
