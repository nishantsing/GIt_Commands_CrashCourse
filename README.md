# Git_Commands_CrashCourse

- [Git Docs](https://git-scm.com/doc)
- - Tottoise Git

## Basic Commands

- git init
- git status
- git log || git log --oneline
- git add . || git add file1.ext file2.ext
- git commit -m "your_message" || git commit//to type big paragraph messages

- git commit -a -m "message" // adds all the changes to stage and commit them

### Amending Commits
- updates just the previous commit
- you can fix commit message or forgot to add some file, you can add that file using git add file1 and git commit -- amend

- git commit --amend

## Branches

HEAD - refers to last commit on master branch(last commit of any branch)

- master branch is default branch when we do git init.
- Github changed from master to main as default.
- git branch // views all branches
- git branch <branch-name> // create branch with that name(shouldn't include spaces) based upon the current HEAD, just makes the branch and doesn't switch to it
  - git branch bugfix
- git switch <branch-name> // switch to that branch and HEAD points to its last commit, newer command as compared to git checkout <branch-name>
  - git switch -c <branch-name> // creates and switches to that branch
  git switch bugfix, git switch master
- git checkout <branch-name> // It does lot more(restore working tree files) than just switching branches  
  - git checkout -b <branch-name>
- NOTE: Commit/Stash before switching to another branch. (otherwise you get error or sometimes dont)
  - If you have some unstaged changes which is not in conflict with other branches like a new file and you dont commit or stash that change and switch, you wont get error and that file will be visible in the switched brach as well.

- git branch -d  <branch-name> // cannot delete the branch you switched in
- git branch -m <branch-name>// you need to be switched in the branch you want to rename

## Merging

- Fast Forward merge (The receiving branch is the branch from which other branch was created and receiving branch dont have any new commits after creating other branch)
  - Switch to the branch you want to merge the changes into (the receivng branch)
  - Use the git merge <branch-name> command to merge changes from a specific branch into the current branch.

- If the receiving branch(master) already has commit ahead of the branch created from the master, then its not a fast forward merge and new merge commit is created. If the commit that is ahead of the other branch in master is conflicting then we will get merge conflict.\
- deletion of same file, or changing of same lines in same file.
 
## Git Diff

- gives you change from last commit and new changes that are not commited.

- git diff //list changes in the working director that are not staged(unstaged).
- git diff HEAD // list all changes(staged+unstaged) in the working directory since last commit
  - git diff HEAD [filename.ext] [filename2.ext] ...
- git diff --staged || git diff --cached // diff between last commit and staging area
  - git diff --staged [filename.ext] ...
- git diff branch1 branch2 || git diff branch1..branch2 // comparing changes between 2 branches.
- git dif commit1 commit2 || git diff commit1..commit2 // comparing changes between 2 commits.

## Stashing
- git stash || git stash save// uncommitted chagnes(staged+unstagd)
- git stash pop
- git stash apply //apply but also keep it in stash as well without poping from stash.
  - git stash apply stash@{2}
- git stash list // list the stashes
- git stash drop stash@{2}
- git stash clear// clears the stash completely

## Undoing changes and Time Traveling

## .gitignore
- To ignoring files.


## Things to keep in mind.
- keep your commits atomic "one feature, one bug or one component" in a commit
- commit messages present tense and commanding or giving order.


## setting up user 

- git config --global usr.name "Name"
- git config --global user.email "email@xyz.com'

## Setting up editor from vm to vscode
- git config --global core.editor "code --wait"

## GUI (GitKraken)


## .git directory

ls -a
cd .git
cat HEAD

refs - heads(every file for the branches) -master(file with last commit)

- git log
