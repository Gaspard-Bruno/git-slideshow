
class: center, middle
title: Git 101

# Git 101*
#### *for dummies

---

# Topics

  - What is Git
  - Git Workflows
  - Cool Git Commands
  - Git GUI's
  - Questions

---
# Git 101
## What is Git ?
- Git is a Distributed Version Control Systems (DVCS), much like Mercurial or SVN.
  - Due to its distributed nature, it allows users to work offline and always keep a copy of a repo's history in their machine.****
- It is used for tracking changes in source code during software development. It is designed for coordinating work among programmers, but it can be used to track changes in any set of files.
- It is free and open source.

![Centralized vs Distributed](http://1.bp.blogspot.com/-e47rFnZpPjY/Vnl4O9KMwuI/AAAAAAAAEIU/mK3le2R_HOk/s1600/2-comparison.PNG)
---
# Git 101
## How does it work ?
- Git basically tracks the history of file changes.
- Whenever we want to save a 'snapshot' of our code, we do a `commit` in a *repository*.
  - When we commit, git saves the changes that were applied to the original file. (not the actual file)
- All git operations are kept in your machine for a certain amount of time and are available through `git reflog`
  - *Due to this, it is very hard to permanently delete your work*
---
# Git Workflows
## Basic Workflow
![Basic git flow](https://buddy.works/blog/images/basic.png)
### Commands used
- `git init` / `git clone`
- `git add`
- `git commit -m "COMMIT MSG"`
- `git push origin BRANCH_NAME "COMMIT MSG"`
---
# Git Workflows
## Basic Workflow
The idea is simple: there is one central repository.
Each developer clones the repo, works locally on the code, makes a commit with changes, and push it to the central repository for other developers to pull and use in their work.
- The basic workflow can work fine if you're the only developer working on a project at a given time.
- Issues arise if 2 developers do changes to the code and push their code at the same time.
- Developers can align between them when each pushes the changes. Keeping the commits in a single branch.
- Enter feature branch workflow
---
# Git Workflows
## Feature Branch Workflow
![Feature branch workflow](https://buddy.works/blog/images/feature-branch.png)
### Commands used
- `git fetch origin`
- `git checkout -b "NEW BRANCH NAME"`
- `git checkout "BRANCH NAME"`
- `git merge "NEW BRANCH NAME"`
---
# Git Workflows
## Feature Branch Workflow
- For each new functionality, a new  branch should be created.
- This new branch will be where we develop and test a new feature.
- Once the feature is done, the branch is merged/rebased onto the master branch.
- This ensures the developers can work simutaneously in two different functionalities and merge them whenever without having to align timings.
---
# Git Workflows
## Rebase vs Merge
![Rebase vs Merge](https://miro.medium.com/max/875/1*pzT4KMiZDOFsMOKH-cJjfQ.png)
- `git rebase` solves the same problem as `git merge`. Both of these commands are designed to integrate changes from one branch into another branch—they just do it in very different ways.

| Merge                                  | Rebase                              |
| -------------------------------------- | ----------------------------------- |
| 1 Merge Commit                         | No extraneous commits               |
| Non-desctructive operation             | Re-writes commit history            |
| Commit history are in feature branches | Single line branch with all commits |
---
# Git Workflows
## Golden Rule of Rebasing
**There are two trade-offs for the pristine commit history the rebase workflow provides: safety and traceability.**
#### The golden rule of git rebase is to never use it on public branches.
- The rebase moves all of the commits in master onto the tip of feature.
- The problem is that this only happened in your repository.
- All of the other developers are still working with the original master.
- Since rebasing results in brand new commits, Git will think that your master branch’s history has diverged from everybody else’s.
- You will need to **Force Push**
---
# Git Workflows
## Force Push
- If you try to push the rebased branch back to a remote repository, Git will prevent you from doing so because it conflicts with the remote branch. *only appliable if you did pushes in-between commits*
- But, you can force the push to go through like so:

`git push origin <BRANCH> -f` OR `git push origin <BRANCH> --force`
- This overwrites the remote branch to match the rebased one from your repository. So, be very careful to use this command only when you know exactly what you’re doing.
- `git pull --rebase` does a pull but rewinds your local commits on top of the target branch
---
# Real Life Examples
## Merge vs Rebase
![Rebase vs Merge](images/ss1.png)
In here we have a branch, `discounts` that's forked from `master` some commits ago. It was recently updated and was ready to merge with `master`.
If we'd rebased `discounts` we'd end up with `master` + our comit(s). If we merged our branch into master and we'd get a single commit with all the changes.
#### What happened
![Rebase vs Merge](images/ss2.jpg)
---
# Cool Git Commands
| Command                                                 | Result                                                      |
| ------------------------------------------------------- | ----------------------------------------------------------- |
| `git commit --amend --no-edit`                          | Ammends without editing the previous commit msg             |
| `git fetch origin && git rebase origin/master`          | Fetches the main branch and winds your changes on top of it |
| `git log -1`                                            | Shows last commit                                           |
| `git checkout <COMMIT_SHA> -- <PATH_TO_FILE>`           | Resets a file to the state it was in the previous commit    |
| `git cherry-pick <COMMIT_SHA>`                          | Cherrypick a single commit                                  |
| `git cherry-pick <FIRST_COMMIT_SHA>..<LAST_COMMIT_SHA>` | Cherrypick a range of commits                               |
| `git config --global credential.helper 'cache --timeout 43200'` | Save your HTTPS credentials for 24hours |
| `git commit —amend —no-edit && git push origin`                 | Quick ammend and push to origin         |
| `git reset HEAD`                                                | Unstage current changes                 |
---
# Cool Git Commands
### Change default git editor
#### VS Code
`git config --global core.editor "code -w"`
#### Sublime
`git config --global core.editor "subl"`
### Purge merged branches
`git checkout <BRANCH_NAME> && git branch --merged | grep -v '\\*' | xargs -n 1 git branch -d`
### Panic Button
`git reflog`
---
# Git GUI's
- `gitk`
- Gitkraken
- Sourcetree
- Fork
- Tortoise Git
- Git Cola
---
# Questions
![404](https://cdn1.iconfinder.com/data/icons/internet-technology-and-security-2/128/77-512.png)
#### Doubts not found
