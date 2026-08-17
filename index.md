# Progress tracker

## Day 1 (August 12)

Read about `git init`, `git clone`, `git config`, `git alias`, `git add`, `git commit`, `.gitignore`, `git fetch`, `git pull` and `git push`.

### `git init`

- `git init --bare <directory>`: Initialize an empty Git repository, but omit the working directory.
- `git init <directory> --template=<template directory>`: Initialize a new Git repository and copy files from the  `＜template_directory＞` into the repository.
- `git init --quiet`
- `git init --separate-git-dir=<dir>`

### `git clone`

- `git clone <repo> <directory>`
- `git clone <repo> --branch <tag>`
- `git clone --depth 1`: shallow clone
- `git clone --bare` and `git clone --mirror` (?)

### `git config`

- `git config --[local/global/system] user.[name/email] <value>`

### `git add`

- `git add -p`: Begin an interactive staging session that lets you choose portions of a file to add to the next commit.

### `git commit`

- `git commit -a`: Commit a snapshot of all changes in the working directory. This only includes modifications to tracked files.

### `git stash`

- `git stash` and `git stash [pop/apply]`
- `git stash` will not stash new files in your working copy that have not yet been staged and files that have been ignored.
- `git stash save "message"`
- `git stash list`
- `git stash pop stash@{2}`
- `git stash drop stash@{1}` and `git stash clear`

### `.gitignore`

- [Git Ignore Patterns](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)
- **Ignoring a previously committed file**:
    1. `echo debug.log >> .gitignore`
    2. `git rm --cached debug.log`
    3. `git commit -m "Start ignoring debug.log"`
- **Committing an ignored file**: `git add -f debug.log`
- **Debugging `.gitignore` files**: `git check-ignore -v debug.log`
  
  The output shows:
  `<file containing the pattern>:<line number of the pattern>:<pattern>  <file name>`

### `git fetch`

- `git fetch <remote>`: Fetch all of the branches from the repository. This also downloads all of the required commits and files from the other repository.
- `git fetch <remote> <branch>`: Only fetch the specified branch.
- `git fetch --all`: Fetches all registered remotes and their branches.
- `git fetch --dry-run`: It will output examples of actions it will take during the fetch but not apply them.

### `git pull`

- `git pull` = `git fetch` + `git merge`
- `git pull --rebase`
- `git pull --no-commit`: Unlike `git fetch`, it modifies the local working branch, but does not create an automatic commit.

### `git push`

- `git push <remote> --force`: 😱
- `git push <remote> --tags`: This flag sends all of your local tags to the remote repository as tags are not automatically pushed.
- **Deleting a remote branch or tag**: `git branch -D branch_name` followed by `git push origin :branch_name`

## Day 2 (Aug 13)

Read about `git tag`, `git log`, `git branch`, `git merge`, `git reset`, `git revert`, `git reflog` and `git rebase`.

### `git tag`

- `git tag <tagname> <commit_hash>`: Lightweight tags.
- `git tag -a <tagname>`: Annotated tags store extra meta data such as: the tagger name, email, and date.
- `git tag -l <wildcard>`: List tags with wildcard
- In the event that you must update an existing tag, the `-f FORCE` option must be used.
- `git push --tags`: 👍

### `git checkout`

- `git checkout -b ＜new-branch＞ ＜existing-branch＞`

### `git revert`

- It will create a new commit with the inverse of the last commit.
