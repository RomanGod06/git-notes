# 🧭 Git Command Hierarchy Map

This map visualizes how Git commands interact with different parts of the system. Think of Git in **5 Logical Layers**, moving from setup to advanced maintenance.

---

## 🧠 Visual Structural Summary
A quick bird's-eye view of the command structure.

```text
GIT SYSTEM
│
├── 1️⃣ Setup & Config
│   ├── init (start here)
│   ├── clone (download)
│   └── config (identity)
│
├── 2️⃣ Core Workflow (The Daily Cycle)
│   ├── status (where am I?)
│   ├── add (stage files)
│   ├── commit (save snapshot)
│   ├── log (history)
│   └── diff (what changed?)
│
├── 3️⃣ Branching & History
│   ├── branch (create/delete)
│   ├── switch / checkout (move)
│   ├── merge (combine)
│   ├── rebase (rewrite)
│   └── cherry-pick (copy commit)
│
├── 4️⃣ Collaboration (Remote)
│   ├── remote (connection)
│   ├── fetch (download info)
│   ├── pull (download + merge)
│   └── push (upload)
│
└── 5️⃣ Advanced & Maintenance
    ├── stash (pause work)
    ├── tag (release version)
    ├── reset / revert (undo)
    ├── clean / gc (cleanup)
    └── submodule / worktree (complex projects)
