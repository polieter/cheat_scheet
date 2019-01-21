# Git cheat sheet
Simple git cheat sheet, base on great [udacity git course](https://classroom.udacity.com/courses/ud123) for beginners and [Learn Git with Bitbucket Cloud](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud).

# Table of content

- [Git cheat sheet](#git-cheat-sheet)
- [Table of content](#table-of-content)
- [Git log, checking history of repo.](#git-log-checking-history-of-repo)
  - [git log](#git-log)
- [Git commit](#git-commit)
- [Git tag](#git-tag)
- [Git branching](#git-branching)
- [Git merge](#git-merge)
- [Git undoing changes](#git-undoing-changes)
  - [Changing The Last Commit](#changing-the-last-commit)
  - [Git revert](#git-revert)
  - [Git reset](#git-reset)
- [Git collaborating](#git-collaborating)
  

# Git log, checking history of repo.

```bash
git status
git log
```
## git log
```bash
git log --oneline #log all commit in one line
git log --stat #log all commit and changed files
git log -p #log all commit and show change in commit

git log --oneline --graph --all
```

# Git commit

```bash
git add . #move all changed file from Working Directory to the Staging Index
git commit -m "Commit message show" #commit
git diff #Show changes that have been made but haven't been committed, yet.
```
Remember about .gitignore file :)

# Git tag
```bash
git tag -a v0.1 -m "tag message" #create new tag
git tag -d v0.1 #delete tag
```

# Git branching
```bash
git branch #show branch
git branch new-branch master #create new-branch
git checkout new-branch #switch to new-branch
git checkout -b second-branch #create and switch to second-branch
git branch -d new-branch #delete new-branch
```

# Git merge
```bash
git merge second-branch #merge second-branch
```

# Git undoing changes

[Git undoing changes](https://www.atlassian.com/git/tutorials/undoing-changes) another reference.

## Changing The Last Commit
```bash
git commit --amend

# Edit hello.py and main.py git add hello.py git commit
# Realize you forgot to add the changes from main.py git add main.py
git commit --amend --no-edit
```

## Git revert 
```bash
git revert <SHA-of-commit-to-revert>
```

## Git reset
Reverting creates a new commit that reverts or undo a previous commit. Resetting, on the other hand, erases commits!

```bash
git reset <reference-to-commit>
```
three flags:
- `--mixed` default (unstages committed changes)
- `--soft` (moves committed changes to the staging index)
- `--hard` (erase commits)


You've got to be careful with Git's resetting capabilities. This is one of the few commands that lets you erase commits from the repository. If a commit is no longer in the repository, then its content is gone.

To alleviate the stress a bit, Git does keep track of everything for about 30 days before it completely erases anything. To access this content, you'll need to use the [```git reflog```](https://www.atlassian.com/git/tutorials/rewriting-history) command.

# Git collaborating

- [```git remote```](https://www.atlassian.com/git/tutorials/syncing)
- [```git fetch```](https://www.atlassian.com/git/tutorials/syncing/git-fetch)
- [```git push```](https://www.atlassian.com/git/tutorials/syncing/git-push)
- [```git pull```](https://www.atlassian.com/git/tutorials/syncing/git-pull)
