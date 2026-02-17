# 🧠 Git Internals: The Complete Architecture Guide

> **"Git is a content-addressable filesystem with a VCS user interface written on top of it."**
> — *Linus Torvalds*

This guide deconstructs Git into its raw components. We will bypass the "Porcelain" commands (like `add`, `commit`) and look at the "Plumbing" (the internal machinery).

---

## 🏗️ Part 1: The `.git` Directory
When you run `git init`, Git creates a `.git` hidden folder. This **IS** your repository. If you delete this folder, you lose your project history.

### 📂 Directory Structure
| File/Folder | Purpose |
| :--- | :--- |
| **`HEAD`** | A text file containing the reference to the current branch. |
| **`config`** | specific configuration (user settings, remote URLs). |
| **`index`** | A binary file acting as the **Staging Area**. It stores file info (metadata) for the next commit. |
| **`objects/`** | The "Database." Stores all content (Blobs, Trees, Commits, Tags). |
| **`refs/`** | Stores pointers (branches, tags, remotes). |
| **`hooks/`** | Scripts triggered by actions (e.g., `pre-commit`). |

---

## 🧩 Part 2: The Object Model (The Database)
Git stores data in a **Key-Value Store** located in `.git/objects`.
* **Key:** SHA-1 Hash (40-character string).
* **Value:** Compressed data.

There are only **4 types of objects** in Git.

### 1️⃣ Blob (Binary Large Object)
* **What it is:** The **content** of a file.
* **What it lacks:** It has NO filename and NO permissions.
* **Example:** If you have two files, `README.md` and `INTRO.txt`, containing the exact same text "Hello World", Git stores **one** blob.
* **Plumbing Command:** `git hash-object -w <file>`

### 2️⃣ Tree
* **What it is:** A directory listing.
* **Function:** It maps **filenames** to **Blob hashes** (or other Tree hashes).
* **Structure:**
    ```text
    100644 blob a906cb2...   README.md
    100644 blob 8f94139...   main.py
    040000 tree 99f1a6d...   lib/
    ```
* **Analogy:** A Tree is like a folder in your OS.

### 3️⃣ Commit
* **What it is:** A snapshot of the project at a specific time.
* **Content:**
    1.  Pointer to a **Tree** (the root directory of the project).
    2.  Pointer to **Parent Commit(s)** (the previous history).
    3.  **Author** & **Committer** info (name, email, timestamp).
    4.  **Commit Message**.
* **Visualization:**
    
    ```text
    tree 3b18e512dba79e4c8300dd08aeb37f8e728b8dad
    parent 22591732e7330756778647000213821038213890
    author John Doe <john@example.com> 1640995200 +0000
    committer John Doe <john@example.com> 1640995200 +0000

    Initial commit
    ```

### 4️⃣ Tag (Annotated)
* **What it is:** A persistent pointer to a commit.
* **Content:** Points to a commit hash + contains a message and GPG signature.
* **Difference:** Branches move; Tags do not.

---

## 📍 Part 3: References (The Pointers)
If Git only had hashes (`a1b2c3d...`), it would be impossible to use. **References (Refs)** are human-readable names that point to these hashes.

### 🌿 Branches
* **Location:** `.git/refs/heads/`
* **Internal Definition:** A text file named (e.g., `main`) containing **only** a commit hash.
* **Example:** content of `.git/refs/heads/main`:
    `22591732e7330756778647000213821038213890`
* **Operation:** When you "commit", Git updates this file with the new commit hash.

### 🎯 HEAD
* **Location:** `.git/HEAD`
* **Internal Definition:** A symbolic reference pointing to the **current branch**.
* **Content Example:** `ref: refs/heads/main`
* **Detached HEAD:** If you checkout a commit directly, HEAD contains a hash instead of a ref path.
    `a1b2c3d4...`

---

## ⚙️ Part 4: The Three Zones (Detailed)



### 1. Working Directory (Sandbox)
* The actual files on your disk.
* Git **does not track** these until you tell it to (`git add`).

### 2. The Index (Staging Area)
* **Location:** `.git/index`
* **Nature:** A binary file.
* **Function:** It is a **manifest** of the files to be included in the next commit.
* **Mechanism:** When you run `git add file.txt`:
    1.  Git compresses the file content into a **Blob**.
    2.  Git stores the Blob in `.git/objects`.
    3.  Git updates `.git/index` to map `file.txt` to that Blob's hash.

### 3. The Repository (History)
* The permanent database of Commits and Trees in `.git/objects`.

---

## 🔄 Part 5: Internal Operations Explained

### What happens when you `git commit`?
1.  Git creates a **Tree object** from the current Index.
2.  Git creates a **Commit object** pointing to that Tree.
3.  The Commit object lists the current `HEAD` commit as its **Parent**.
4.  Git updates the current branch file (e.g., `refs/heads/main`) to point to the new Commit hash.

### What happens when you `git checkout <branch>`?
1.  Git looks up the hash inside `refs/heads/<branch>`.
2.  Git reads the **Commit** object for that hash.
3.  Git reads the **Tree** object referenced by that commit.
4.  Git updates the **Index** to match that Tree.
5.  Git updates your **Working Directory** files to match the Index.
6.  Git updates `HEAD` to point to `refs/heads/<branch>`.

### What happens when you `git merge`?
* **Fast-Forward:** If the target branch is directly ahead of the current branch, Git simply moves the pointer. No new object is created.
* **True Merge (3-Way):**
    1.  Git finds the "Best Common Ancestor" (Base).
    2.  Git compares **Current** state vs. **Base**.
    3.  Git compares **Target** state vs. **Base**.
    4.  Git combines the changes into a **New Commit** with **Two Parents**.

---

## 📦 Part 6: Storage Optimization (Packfiles)
Initially, Git stores every version of every file as a separate **Loose Object**. This is inefficient.

### Garbage Collection (`git gc`)
Periodically, Git compresses these loose objects into **Packfiles**.
* **Loose Object:** Full file content (zlib compressed).
* **Packfile:** Stores one full version + **Deltas** (differences) for other versions.
* **Result:** This is why a Git repo can sometimes be smaller than the source code itself!

---

## 🛠️ Part 7: Plumbing Commands (Try it yourself!)
Use these commands to see the internals in action.

| Command | Description |
| :--- | :--- |
| `git cat-file -p <hash>` | Print the content of an object (Blob, Tree, or Commit). |
| `git cat-file -t <hash>` | Tell the type of an object. |
| `git ls-files --stage` | View the contents of the Index (Staging Area). |
| `git rev-parse HEAD` | See the raw hash that HEAD points to. |
| `git hash-object <file>` | Compute the SHA-1 hash of a file without saving it. |

---
