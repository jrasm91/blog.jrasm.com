---
title: Git Cheetsheet
description: Cheetsheet for git commands
date: 2022-03-08
publishDate: 2022-03-08
tags: [git]
showReadingTime: false
showToc: true
tocOpen: true
---

## Config

Edit git configuration settings.

```bash
# list global config
git config --global --list

# edit global config
git config --global --edit

# default editor (vim, vi, emacs, "code --wait")
git config --global core.editor vim

# default log format (hash, date, name, message, one line, colors)
git config --global format.pretty "format:%C(yellow)%h %Cblue%>(14)%ad %Cgreen%<(16)%aN%Cred%d %Creset%s"

# set user name/email
git config --global user.name "John Smith"
git config --global user.email john.smith@example.com
```

## Commit

Commit related commands.

```bash
# traditional
git commit -m "<message>"

# add message via configured editor
git commit

# add staged files to previous commit
git commit --amend

# add staged files and reuse previous commit message
git commit --amend --no-edit

# undo last commit
git reset HEAD~1

# undo last commit, but keep files as staged
git reset --soft HEAD~1
```

## Diff

View changes.

```bash
# show changes for a commit
git diff <commit>

# show changes between two commits
git diff <commit1> <commit2>
```

## Branch

Work with branches.

```bash
# list branches (* indicates current branch)
git branch

# switch to existing branch
git checkout <branch>

# switch to a new branch
git checkout -b <branch>

# push upstream
git push

# push (and link) to upstream branch
git push --set-upstream origin <branch>

# pull latest changes for current branch
git pull

# rename current branch
git branch -M <new_name>

# rename another branch
git branch -M <branch> <new_name>

# delete branch
git branch -D <branch>
```

## Stash

Save local changes to a "stash" that can be restored later. Great for saving work-in-progress changes. Essentially this creates a temporary commit that can be re-applied in the future (even on another branch or commit).

```bash
# create stash (tracked files with changes)
git stash

# create stash (with both tracked and untracked files)
git stash --include-untracked

# list stashes
git stash list

# restore latest stash
git stash pop
```

## Cherry Pick

Copy a commit onto the current branch.

```bash
git cherry-pick <commit_hash>
```
