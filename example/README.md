# Example: acme-payments-repo

A small project that uses context-db, ready to run. It keeps a usage folder for
the projects that use it, and it reads the usage folder of a project that it
uses itself, the ledger.

```
example/
├── shared/                             standards that "another repository" owns
│   ├── coding-standards/
│   └── git-standards/
├── acme-ledger-repo/                   a project that acme-payments uses
│   └── okf/acme-ledger-usage/          its usage folder; the rest is left out
└── acme-payments-repo/                 the example project
    ├── AGENTS.md
    ├── .claude/skills/context-db       symlink to ../../skill/context-db
    └── context-db/
        ├── configuration/              settings.md finds the ledger's usage folder;
        │                               ON_PROMPT.md carries a PCI reminder
        ├── acme-payments-project/      the project folder: project knowledge
        │   ├── architecture.md
        │   ├── api-reference.md
        │   ├── data-model/
        │   ├── acme-payments-usage/    its usage folder: usage knowledge
        │   └── wip/                    wip.md lists refund-endpoint.md
        ├── coding-standards -> ../../shared/coding-standards
        └── git-standards -> ../../shared/git-standards
```

Try it:

```bash
cd example/acme-payments-repo
python3 .claude/skills/context-db/context-db.py prompt "add a refund endpoint"
python3 .claude/skills/context-db/context-db.py update
python3 .claude/skills/context-db/context-db.py wip --list
python3 .claude/skills/context-db/context-db.py maintain
python3 .claude/skills/context-db/context-db.py toc
python3 .claude/skills/context-db/context-db.py toc context-db/coding-standards
python3 .claude/skills/context-db/context-db.py toc ../acme-ledger-repo/okf/acme-ledger-usage
python3 .claude/skills/context-db/context-db.py toc --check
```
