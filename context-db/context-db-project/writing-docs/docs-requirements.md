---
type: Convention
description:
  What the owner requires of the docs pages and the README — OKF up front, the
  install prompt first, one-word Title Case navigation, no Why or migration
  page, no logo, no call-to-action buttons, light mode, a restrained look, and
  a Benefits section that is not to be rewritten.
---

# What the owner requires of the docs

- The head of the home page and of the README must say that context-db is built
  on the Open Knowledge Format.
- Early on both, there must be a link to the explainer page,
  [docs/okf.md](../../../docs/okf.md). That page covers what OKF is, a short
  history with a hyperlink for every entry, and which parts context-db uses.
- Both must say plainly that context-db is a set of skills.
- The theme should be colorful, "a bit snazzier than usual". Pages open in
  light mode; the owner asked for "white docs".

Added by the owner on 2026-11-11:

- The home page, the README, and the Setup page lead with the prompt a user
  pastes into their agent to install context-db from the GitHub repository.
  People must be able to point their agent at the repository and have it do the
  setup.
- Labels in the top navigation are Title Case, and one word where possible.
  "Get started" and "Knowledge base" were rejected; they became Setup and
  Layout.
- There is no page for "why" and none for migrating from v0.0. The why is a
  short section at the end of the home page and the README. Migration is the
  owner's own task; its guide stays in this knowledge base and out of the docs.
- On the Commands page, each command's section is headed by the full command,
  such as `/context-db update`.
- The home page and the README open with Two kinds of knowledge: the two
  terms, how a project reads another project's usage folder, and that its own
  project knowledge comes first. The owner asked on 2026-11-22 for this "right
  at the start". A short Example of `prompt` and `update --push` follows it,
  before Install. It is static; the owner asked for "not animated".
- Sharing is a section of the Layout page, not a page of its own.
- No logo in the header. The name there and the home page title both read
  `/context-db`.
- No call-to-action buttons under the intro. The owner found the two pill
  buttons "really tired, very much what agents look like". The intro's own link
  to the OKF page and the Install section do that job.
- The footer keeps the theme's Sphinx and PyData credits and nothing else, on
  one small line. The owner had the copyright line removed and the footer
  halved because it "looks really bad on a phone". Check a footer change at
  phone width.
- The Commands page ends with "How it all fits together": what the script
  sends for each command, section by section, next to the ON files. The owner
  wants it "crystal clear how the whole system works", and wants this stressed:
  context-db "is nothing more than some canned context alongside user
  controlled context in the ON files", sent on demand when the user invokes a
  command.
- The home page and the README have a Benefits section after Example, which
  links to that section. The owner wrote its wording by hand on 2026-11-11,
  after rejecting a long list and then a list of one-liners: two or three plain
  sentences a bullet. Fix typos there, but do not rewrite it.
- The commands section of both opens with the whole API in one block, and the
  note that a command is a starting point. See
  [command-set.md](../design-decisions/command-set.md).
- Colorful, but restrained. The owner had every gradient halved, the home page
  title cut down, and all type set 10% smaller, because the defaults read "a
  little big". The name in the header was already the right size. Lean smaller
  and quieter when adding to the look.

Follow [voice.md](./voice.md) for every page.
