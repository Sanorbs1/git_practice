# Git Practice – Local, Branching, and History

This repository is for practicing core Git commands: init, add/commit, amend, branching, merging, rebase, and pushing to a remote. It also notes a few troubleshooting steps (DNS, editor, rebase issues). [web:102][web:104]

## 1. Initialize and first commit

### Steps
1. Create a project folder and initialize Git:
   ```bash
   git init
   ```
2. Create a file (for example `README.md` or `index.html`).
3. Check status:
   ```bash
   git status
   ```
4. Stage and commit:
   ```bash
   git add .
   git commit -m "Initial commit"
   ```

### Goal
Understand working directory → staging → local repository using `git add` and `git commit`. [web:104]

---

## 2. Staging and `commit --amend`

### Task A: Stage changes iteratively
1. Edit `notes.txt` and add a first line.
2. Stage and commit:
   ```bash
   git add notes.txt
   git commit -m "Add first note"
   ```
3. Edit `notes.txt` again (add a second line).
4. Stage and commit again:
   ```bash
   git add notes.txt
   git commit -m "Explain restaging after edits"
   ```

Learn that any new changes after a commit must be staged again before the next commit. [web:12][web:15][web:18]

### Task B: Fix the last commit with amend
1. Fix a typo or add a small extra change in the same file.
2. Stage it:
   ```bash
   git add notes.txt
   ```
3. Amend the last commit:
   ```bash
   git commit --amend
   ```

Use amend when you need to correct the latest commit’s message or content. [web:57][web:59]

---

## 3. Handling the commit editor (Vim)

When you run `git commit` without `-m`, Git opens an editor (often Vim) with lines like:

```text
Please enter the commit message for your changes.
Lines starting with '#' will be ignored, and an empty message aborts the commit.
```

### How to use it
- Write your commit message at the top, above the `#` lines.
- Press `Esc`, type `:wq`, press `Enter` to save and finish the commit.
- Press `Esc`, type `:q!`, press `Enter` to exit without saving. [web:21][web:23][web:25]

If you prefer to avoid the editor, use:

```bash
git commit -m "Your message here"
``` [web:22]

---

## 4. Branching and creating files per branch

### Create and switch to a branch
```bash
git switch -c feature/style-page
```
or
```bash
git checkout -b feature/style-page
``` [web:72]

### Create a branch-specific file
1. While on `feature/style-page`, create a file:
   ```bash
   echo "<h1>Style page</h1>" > style.html
   ```
2. Stage and commit:
   ```bash
   git add style.html
   git commit -m "Add style.html in feature branch"
   ```

Changes stay isolated in that branch until merged into `main`. [web:67][web:72]

---

## 5. Rename `master` to `main`

If the default branch is `master` and you want `main`:

```bash
git branch -m master main
git push -u origin main
git push origin --delete master
```

Optionally set `main` as the default in the hosting service settings and configure new repos globally: [web:52][web:56]

```bash
git config --global init.defaultBranch main
```

---

## 6. Pulling correctly from remote

To update your branch from remote `main`:

```bash
git pull origin main
```

Remember:
- `origin` = remote name.
- `main` = branch name.
- `git pull main` alone is invalid because Git expects a remote name first. [web:90][web:95]

---

## 7. Pushing local repo to remote

After `git init` and some commits:

```bash
git remote add origin <repo-url>
git branch -M main          # if you use main
git push -u origin main
```

This connects your local repository to the remote and uploads your history. [web:31][web:32][web:36]

---

## 8. Basic rebase and cleanup

### Keep a feature branch up to date with main
From your feature branch (for example `stylef`):

```bash
git pull --rebase origin main
```

This rebases your branch on top of the latest `main` commits, rewriting your branch history to be clean and linear. [web:57][web:61][web:99]

### Fix a stuck rebase state
If `git rebase --abort` or `git rebase --quit` fails with messages about `.git/rebase-merge`:
1. Close editors and terminals working in that repo.
2. Delete the `.git/rebase-merge` folder manually.
3. Run:
   ```bash
   git status
   ```
to confirm the repository is clean. [web:39][web:44]

---

## 9. DNS configuration troubleshooting (work machine)

If you see DNS errors (sites not resolving, “DNS server not responding”):

1. Restart router and PC. [web:86][web:87]
2. Flush DNS cache (Windows):
   ```bash
   ipconfig /flushdns
   ```
3. Reset network stack:
   ```bash
   ipconfig /release
   ipconfig /renew
   netsh winsock reset
   ```
4. Set a public DNS (e.g. Google or Cloudflare):
   - 8.8.8.8 and 8.8.4.4
   - 1.1.1.1 and 1.0.0.1 [web:74][web:79][web:87]

If office DNS is misconfigured, report it to IT/HR with the error message and time of issue. [web:74][web:84]

---

## 10. Quick command checklist

- Init & first commit:
  - `git init`
  - `git status`
  - `git add .`
  - `git commit -m "message"`

- Amend:
  - `git add <file>`
  - `git commit --amend`

- Branching:
  - `git switch -c <branch>`
  - `git switch <branch>`
  - `git merge <branch>`

- Remote:
  - `git remote -v`
  - `git remote add origin <url>`
  - `git push -u origin main`
  - `git pull origin main` [web:52][web:104]

---

Happy practicing! Each section above can be turned into a small lab: follow the commands, then run `git log`, `git status`, and `git branch` to see what changed after each step. [web:100][web:102]
```

If you tell me your actual branch names and files (like `stylef`, `index.html`), I can customize this README exactly to your project.
