# Git Bash — Learn with Best

This is my Git and Git Bash learning repository.

**Author:** Anshul

The purpose of these notes is to understand Git commands, Git Bash, GitHub collaboration, and version control through practical examples.

---

## 1. Git Bash and Basic Terminal Commands

Git Bash provides a Bash terminal on Windows. It lets us run Git commands and many Unix-style terminal commands.

### Check the current directory

```bash
pwd
```

**Meaning:** Prints the path of the current working directory.

### List files and folders

```bash
ls
```

Shows visible files and folders.

```bash
ls -a
```

Shows hidden files and folders too, including `.git`.

```bash
ls -l
```

Shows detailed file information in a list.

```bash
ls -la
```

Shows detailed information, including hidden files.

### Change directories

```bash
cd folder_name
```

Moves into a folder.

```bash
cd ..
```

Moves one directory up.

```bash
cd ~
```

Moves to the user's home directory.

### Create a folder or file

```bash
mkdir folder_name
```

Creates a directory.

```bash
touch README.md
```

Creates an empty file if it doesn't exist. If it already exists, `touch` updates its modification timestamp.

### Windows PowerShell alternatives

These commands are for PowerShell, not Git Bash:

```powershell
Get-ChildItem -Force
ls -Force
```

PowerShell uses `-Force` to include hidden items. In Git Bash, use `ls -a`.

### Common Windows file attributes

When working with Windows files, you may encounter:

- **Attributes:** Properties assigned to a file or folder.
- **Directory:** An item that represents a folder.
- **File:** An item that stores data.
- **Hidden:** An item normally hidden from standard directory listings.
- **ReadOnly:** An attribute that indicates a file should be treated as read-only by applications that respect it.
- **System:** An attribute used by Windows for system-related files.

To inspect Windows file attributes in PowerShell:

```powershell
Get-ChildItem -Force | Select-Object Name, Attributes
```

These attributes are separate from Git's version-control tracking.

---

## 2. Git Basics

### Check the installed Git version

```bash
git --version
```

Shows the installed Git version.

### Configure your Git identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Git records this identity in new commits. Use the name and email you want associated with your commits.

Check the configuration:

```bash
git config --global --list
```

### Initialize a repository

```bash
git init
```

Initializes a Git repository in the current directory.

Use this when starting version control for a folder that is not already a repository. You do not need to run it for every new folder or repeatedly inside an existing repository.

To initialize a repository with a `main` branch:

```bash
git init -b main
```

### Check repository status

```bash
git status
```

Shows the current branch, staged changes, unstaged changes, and untracked files.

### Add files to staging

```bash
git add README.md
```

Stages a specific file.

```bash
git add .
```

Stages eligible changes under the current directory, including additions, modifications, and deletions. Ignored files are not staged.

### Commit changes

```bash
git commit -m "Add Git notes"
```

Creates a commit from the staged changes.

A commit is a saved snapshot of the staged version-controlled changes, along with metadata such as the author and commit message.

### View configured remotes

```bash
git remote -v
```

Shows the remote repository names and their fetch/push URLs.

### Add a remote repository

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
```

Adds a remote named `origin`.

**Important:** `git remote add` and `git status` are separate commands. Do not combine them as `git remote add git status`.

### Push changes to GitHub

```bash
git push -u origin main
```

Pushes the local `main` branch to `origin` and sets its upstream tracking branch.

After the upstream is configured, you can usually use:

```bash
git push
```

This does not force every future push to use `main`; it sets tracking for the current branch.

---

## 3. Working Tree and Staging

Git work normally involves three areas:

1. **Working tree:** Your current files.
2. **Staging area:** The changes selected for the next commit.
3. **Repository history:** The commits already saved in Git.

### Check what has changed

```bash
git status
```

Shows which files are untracked, modified, staged, or deleted.

```bash
git diff
```

Shows unstaged changes compared with the index.

```bash
git diff --staged
```

Shows staged changes compared with the latest commit.

### Stage and commit selected changes

```bash
git add README.md
git diff --staged
git commit -m "Update README notes"
```

This lets you review the exact changes before committing.

### Unstage a file

```bash
git restore --staged README.md
```

Removes the file from staging while keeping its working-tree changes.

Alternative:

```bash
git reset -- README.md
```

This also unstages the file without discarding its working-tree changes.

### Discard unstaged changes

```bash
git restore README.md
```

**Warning:** This discards the unstaged changes in the file by restoring it from the index. It can destroy work you have not saved elsewhere.

### Stage all eligible changes

```bash
git add .
```

Review the result before committing:

```bash
git status
git diff --staged
```

**Best practice:** Stage and review changes intentionally instead of committing everything blindly.

---

## 4. Clone, Fetch and Pull

These commands are used to work with remote repositories such as GitHub.

### Clone a repository

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
```

Downloads a repository and its history into a new local directory.

Example:

```bash
git clone https://github.com/AnshulHR26/gitnotes_local.git
```

Then move into the repository:

```bash
cd gitnotes_local
```

You normally use `git clone` once when obtaining a local copy of a repository.

### Fetch remote changes

```bash
git fetch origin
```

Downloads updates from `origin` without merging them into your current branch.

Check remote branches:

```bash
git branch -r
```

Compare your branch with the remote-tracking branch:

```bash
git log --oneline HEAD..origin/main
```

This displays commits reachable from `origin/main` that are not reachable from your current `HEAD`.

### Pull remote changes

```bash
git pull
```

Fetches changes from the configured upstream and integrates them into your current branch. Depending on configuration, integration may use a merge or rebase.

To specify the remote and branch:

```bash
git pull origin main
```

Use this when you want to integrate updates from the remote `main` branch into your current branch.

**Important:** `git pull origin main` does not mean “switch to main.” Check your current branch first:

```bash
git branch --show-current
```

**Warning:** Pulling can produce merge conflicts or integrate changes you did not expect. Review your working tree and commit or safely stash important changes before pulling.

### Quick comparison

| Command | Purpose |
|---|---|
| `git clone` | Creates a local copy of a remote repository. |
| `git fetch` | Downloads remote updates without integrating them. |
| `git pull` | Fetches and integrates remote updates. |

---

## 5. Git Log and Commit History

Git history helps you understand what changed and when.

### View commit history

```bash
git log
```

Shows detailed commit history.

```bash
git log --oneline
```

Shows one compact line per commit.

```bash
git log --oneline --graph --all
```

Shows a compact graph of branches and commits.

```bash
git log -5 --oneline
```

Shows the latest five commits.

### Inspect a particular commit

```bash
git show COMMIT_HASH
```

Replace `COMMIT_HASH` with an actual commit hash.

Displays information about the commit and its changes.

### Compare commits

```bash
git diff COMMIT_A COMMIT_B
```

Shows file differences between two commits.

### See which files changed

```bash
git diff --name-only COMMIT_A COMMIT_B
```

Lists filenames that differ between the two commits.

### Find the current commit

```bash
git rev-parse HEAD
```

Prints the full hash of the current commit.

**Tip:** Use `git log --oneline` to find a commit hash before inspecting or reverting a particular commit.

---

## 6. Ignore Files with `.gitignore`

A `.gitignore` file tells Git which untracked files and directories to ignore.

### Create or edit `.gitignore`

Create a file named `.gitignore` in the repository root.

Example contents:

```gitignore
# Python virtual environments
.venv/
venv/

# Python cache
__pycache__/
*.py[cod]

# Environment variables and secrets
.env
.env.*

# Keep an example environment file
!.env.example

# IDE settings
.vscode/

# Logs
*.log
```

Adjust the rules to fit your project. For example, you may choose to commit shared VS Code configuration, so ignoring `.vscode/` is optional.

### Check whether a file is ignored

```bash
git check-ignore -v .env
```

Shows the matching ignore rule for `.env`, if one applies.

### Important: already-tracked files

Adding a file to `.gitignore` does not automatically stop Git from tracking a file that is already tracked.

To stop tracking a file while keeping it on your computer:

```bash
git rm --cached filename
```

For a directory:

```bash
git rm -r --cached directory_name
```

Then commit the change:

```bash
git add .gitignore
git commit -m "Update ignore rules"
```

**Warning:** `git rm` without `--cached` removes the file from the working tree as well as staging its removal. Review the command before running it.

**Security warning:** Never commit passwords, API keys, private keys, or real `.env` secrets. If a secret was already pushed, removing it in a later commit does not erase it from earlier history. Revoke or rotate the exposed secret immediately.

---

## 7. Git Branches and Merging

Branches let you develop changes separately from the main line of work.

### List branches

```bash
git branch
```

Lists local branches.

```bash
git branch -a
```

Lists local and remote-tracking branches.

### Create a branch

```bash
git branch feature1
```

Creates a branch named `feature1` without switching to it.

### Switch branches

```bash
git switch main
```

Switches to `main`.

```bash
git switch -c feature2
```

Creates `feature2` and switches to it.

Older equivalent commands include `git checkout`, but `git switch` is often clearer for branch switching.

### Merge a branch

First switch to the branch that should receive the changes:

```bash
git switch main
git merge feature1
```

This merges `feature1` into the current `main` branch.

**Important:** `git merge feature1` merges into your current branch. It does not automatically switch to `main`.

### Delete a branch

```bash
git branch -d feature1
```

Deletes a local branch if Git considers it safely merged.

```bash
git branch -D feature1
```

Force-deletes a local branch even if it has unmerged changes.

**Warning:** `-D` can cause you to lose the easy reference to unmerged work. Check the branch and its commits before using it.

You cannot delete the branch you are currently on. Switch to another branch first.

---

## 8. Reset, Revert and Undoing Changes

These commands have different effects. Choose carefully.

### Unstage all staged changes

```bash
git reset
```

Unstages staged changes while keeping the working-tree edits.

### Move the current branch back one commit

```bash
git reset HEAD~1
```

Moves the current branch back by one commit. By default, the changes from that commit remain in the working tree as unstaged changes.

### Hard reset

```bash
git reset --hard COMMIT_HASH
```

Moves the current branch to the specified commit and resets the index and working tree to match it.

**Danger:** This can permanently discard uncommitted changes. Verify the commit hash and save any important work before using it.

### Revert a commit

```bash
git revert COMMIT_HASH
```

Creates a new commit that reverses the changes introduced by the specified commit.

For commits that have already been shared with teammates, `git revert` is generally safer than rewriting shared history with `git reset`.

### Quick comparison

| Command | Main effect |
|---|---|
| `git restore --staged FILE` | Unstages a file. |
| `git restore FILE` | Discards unstaged changes in a file. |
| `git reset HEAD~1` | Moves the branch back one commit; keeps changes unstaged by default. |
| `git reset --hard HASH` | Resets branch, index and working tree; potentially destructive. |
| `git revert HASH` | Creates a new commit that reverses an earlier commit. |

---

## 9. Stash — Temporarily Save Uncommitted Work

**Stash is a useful everyday topic.** It allows you to set aside changes temporarily without making a commit.

### Save changes

```bash
git stash
```

Stashes tracked-file changes and restores the working tree to a clean state. By default, untracked files are not included.

### Include untracked files

```bash
git stash -u
```

Includes untracked files as well.

### List stashes

```bash
git stash list
```

Shows saved stashes.

### Apply a stash and keep it

```bash
git stash apply
```

Applies the most recent stash but keeps it in the stash list.

### Apply and remove the stash entry

```bash
git stash pop
```

Applies the most recent stash and normally removes its entry if the application succeeds.

### Apply a specific stash

```bash
git stash apply stash@{1}
```

Applies the stash at index `1` in the stash list.

### Delete a stash entry

```bash
git stash drop stash@{0}
```

Deletes a specific stash entry.

**Warning:** Dropping a stash deletes that saved entry. Confirm you no longer need it first. Stash operations can also cause conflicts when the same lines have changed elsewhere.

**Example workflow:**

```bash
git stash push -u -m "Work in progress"
git switch main
git pull
git switch feature1
git stash pop
```

Use this when you need to change branches or update your work while temporarily setting aside unfinished changes. Check the status and resolve any conflicts afterward.

---

## 10. Authentication and SSH

GitHub authentication lets Git verify that you have permission to access a repository.

### HTTPS remote

An HTTPS remote looks like this:

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
```

Git operations may prompt you to authenticate through a browser or credential manager.

**Important:** GitHub does not accept your regular account password for Git-over-HTTPS authentication. Use a supported sign-in flow or a personal access token when required. Never paste a token into a public repository or share it.

### Check your remote

```bash
git remote -v
```

Displays the remote URLs used for fetch and push.

### Generate an SSH key

Check whether SSH keys already exist:

```bash
ls -al ~/.ssh
```

If you do not already have a suitable key, generate one:

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Follow the prompts. Set a passphrase when possible.

**Warning:** Do not overwrite an existing key unless you understand what uses it. Keep the private key private.

### Start the SSH agent in Git Bash

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

The second command adds the private key to the agent.

### Add the public key to GitHub

Display your public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the public key and add it to your GitHub account under **Settings → SSH and GPG keys**.

Only share the public key (`.pub` file). Never share the private key.

### Test SSH authentication

```bash
ssh -T git@github.com
```

On the first connection, verify GitHub's host fingerprint against its official documentation before accepting it.

### Change a remote from HTTPS to SSH

```bash
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

Then verify:

```bash
git remote -v
```

**Tip:** Choose either HTTPS or SSH based on your workflow. You do not need to set up both just to use Git.

---

## 11. Rebase and Cherry-pick — Optional Advanced Topics

These are useful when you understand commits, branches, merging, and conflict resolution.

### Rebase

Rebase reapplies commits from your current branch on top of another base commit.

Example:

```bash
git switch feature1
git fetch origin
git rebase origin/main
```

This attempts to replay your feature-branch commits on top of the updated remote-tracking `main` branch.

If a conflict occurs:

```bash
git status
```

Edit the conflicting files, then stage the resolutions:

```bash
git add resolved_file.py
git rebase --continue
```

To stop the rebase and return to the state before it began:

```bash
git rebase --abort
```

**Warning:** Rebase changes commit history by creating new commit IDs. Avoid rebasing commits other people are already using unless your team has agreed on that workflow. Do not use `git push --force` casually.

### Cherry-pick

Cherry-pick applies the change introduced by a specific commit to your current branch.

Example:

```bash
git switch main
git cherry-pick COMMIT_HASH
```

Replace `COMMIT_HASH` with the intended commit hash.

If a conflict occurs, resolve the files, stage them, and continue:

```bash
git add resolved_file.py
git cherry-pick --continue
```

To cancel the cherry-pick operation:

```bash
git cherry-pick --abort
```

**Warning:** Cherry-picking creates a new commit on the target branch. The original commit remains in its original history, so cherry-picking is not the same as merging the entire branch.

### Merge vs. rebase vs. cherry-pick

| Command | Purpose |
|---|---|
| `git merge` | Integrates a branch into the current branch, often preserving branch history. |
| `git rebase` | Replays commits onto a new base, creating rewritten commit IDs. |
| `git cherry-pick` | Applies selected commit changes to the current branch. |

**Learning order:** Understand merging first. Learn rebase and cherry-pick after you are comfortable reading commit history and handling conflicts.

---

## 12. Tags and Releases — Optional Advanced Topics

Tags mark specific commits, often to identify release versions.

### List tags

```bash
git tag
```

Lists local tags.

### Create a lightweight tag

```bash
git tag v1.0.0
```

Marks the current commit with `v1.0.0`.

### Create an annotated tag

```bash
git tag -a v1.0.0 -m "First stable release"
```

Creates a tag with a message and tag metadata. Annotated tags are generally preferred for releases.

### Tag a specific commit

```bash
git tag -a v1.0.0 COMMIT_HASH -m "First stable release"
```

Replace `COMMIT_HASH` with the intended commit hash.

### Push a tag to GitHub

```bash
git push origin v1.0.0
```

Pushes that tag to the remote.

To push all local tags:

```bash
git push origin --tags
```

**Warning:** This pushes every local tag, not just the one you intended. Prefer pushing a specific tag when working on a release.

### Delete a local tag

```bash
git tag -d v1.0.0
```

### Delete a remote tag

```bash
git push origin --delete v1.0.0
```

**Warning:** Coordinate with teammates before deleting published tags because they may already rely on them.

### GitHub Releases

A Git tag identifies a point in repository history. A GitHub Release is a GitHub-hosted release page associated with a tag and may include release notes or downloadable assets.

Typical release workflow:

1. Make sure the intended code is committed.
2. Create an annotated tag such as `v1.0.0`.
3. Push the tag.
4. Open the repository on GitHub and create a Release using that tag.
5. Add release notes and any appropriate assets.

---

## 13. Git Collaboration Workflow

This is a common workflow when working with teammates.

### Step 1: Clone the repository

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
```

### Step 2: Update your local main branch

```bash
git switch main
git pull origin main
```

### Step 3: Create a feature branch

```bash
git switch -c feature/add-readme-section
```

### Step 4: Make changes and inspect them

```bash
git status
git diff
```

### Step 5: Stage and commit

```bash
git add README.md
git diff --staged
git commit -m "Add README learning section"
```

### Step 6: Push the feature branch

```bash
git push -u origin feature/add-readme-section
```

The `-u` option configures upstream tracking for this branch.

### Step 7: Open a Pull Request

On GitHub, open a Pull Request from your feature branch into `main`.

A **Pull Request (PR)** asks teammates to review and integrate your changes. It is not the same as `git pull`.

### Step 8: Review and resolve feedback

Make requested changes on your feature branch, commit them, and push the branch again. The Pull Request will update.

### Step 9: Merge the Pull Request

After required reviews and checks pass, merge the PR using your team's chosen method.

### Step 10: Update your local main branch

```bash
git switch main
git pull origin main
```

Optionally delete the local feature branch after verifying that the work has been merged:

```bash
git branch -d feature/add-readme-section
```

### Fork vs. clone

- **Clone:** Downloads a repository to your computer.
- **Fork:** Creates a separate GitHub repository under your account or organization.
- **Pull Request:** Proposes changes from one branch or repository to another.

Forks are especially useful when contributing to projects where you do not have direct write access.

### Merge conflicts

A merge conflict occurs when Git cannot automatically reconcile competing changes. It is not limited to two people editing the exact same line; changes to overlapping sections or certain file operations can also conflict.

To investigate:

```bash
git status
```

Open the conflicted files, review both versions, edit the final intended content, remove conflict markers, and stage the resolved files.

Then continue the operation as appropriate—for example, complete a merge with a commit if Git requests one.

**Important:** Do not blindly choose one side of a conflict without understanding which changes need to be preserved.

---

## 14. Useful Git Commands — Quick Reference

| Command | Purpose |
|---|---|
| `git status` | Check the working tree and staging area. |
| `git add FILE` | Stage a specific file. |
| `git add .` | Stage eligible changes under the current directory. |
| `git commit -m "message"` | Create a commit. |
| `git log --oneline` | View compact commit history. |
| `git diff` | Review unstaged changes. |
| `git diff --staged` | Review staged changes. |
| `git branch` | List local branches. |
| `git switch main` | Switch to `main`. |
| `git switch -c BRANCH` | Create and switch to a branch. |
| `git merge BRANCH` | Merge the named branch into the current branch. |
| `git fetch origin` | Fetch remote updates. |
| `git pull` | Fetch and integrate upstream changes. |
| `git push` | Push to the configured upstream. |
| `git remote -v` | View remote URLs. |
| `git stash` | Temporarily stash tracked-file changes. |
| `git tag` | List tags. |

---

## 15. Common Mistakes to Avoid

1. Running `git init` repeatedly in a repository that already exists.
2. Assuming `git add .` creates a commit or pushes changes to GitHub.
3. Running `git merge feature1` without checking which branch is currently active.
4. Assuming `git push -u origin main` configures every branch to push to `main`.
5. Confusing `git fetch` with `git pull`.
6. Assuming `.gitignore` automatically untracks files that are already tracked.
7. Running `git reset --hard` without checking for uncommitted work.
8. Force-deleting a branch without checking whether its commits are needed.
9. Sharing a private SSH key, password, or API token.
10. Rebasing shared history without coordinating with teammates.
11. Assuming a Pull Request and `git pull` are the same operation.
12. Committing changes without reviewing `git status` and `git diff --staged`.

---

## 16. Recommended Learning Order

### Core topics

1. Git Bash navigation and basic commands.
2. Initialize, stage, commit, and check status.
3. Remote repositories and push.
4. Clone, fetch, and pull.
5. Working tree, staging, and commit history.
6. Branches, merge, and merge conflicts.
7. `.gitignore`, reset, and revert.
8. Stash.
9. Authentication with HTTPS or SSH.
10. Git collaboration workflow and Pull Requests.

### Optional advanced topics

- Rebase and cherry-pick.
- Tags and releases.
- More complex branching strategies and history recovery.

**Practice rule:** Before running a command that changes history or deletes data, inspect the current branch, run `git status`, and understand exactly what the command will change.
