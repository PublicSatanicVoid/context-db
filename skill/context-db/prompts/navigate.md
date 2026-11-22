# How to Navigate Context-db

To see what a folder holds, run:

    {toc_cmd} <folder>

It prints one line for each file and subfolder, with its description. This is
context-db's dynamic index: the listing is built every time it is asked for,
from the files as they are now, so it is never out of date. Use it every time
you look into a folder, now or later in the session, instead of listing the
folder, opening files to see what they are, or reading an `index.md` that the
folder may carry.

- Start with the project folder and the other folders listed under Folders.
- Open a file only when its description says it bears directly on the task.
- Run `{toc_cmd}` on a subfolder only when its description does.
- Skip everything else. Reading widely dilutes what matters.
- Links inside a file are relative to that file.
