# Git cheat sheet
Simple git cheat sheet, base on great [udacity git course](https://classroom.udacity.com/courses/ud123) for beginners.

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
