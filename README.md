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
- git checkout <branch-name> // It does lot more(restore working tree files) than just switching branches, like moving to other commits, restoring things
  - git checkout -b <branch-name>
- NOTE: Commit/Stash before switching to another branch. (otherwise you get error or sometimes dont)
  - If you have some unstaged changes which is not in conflict with other branches like a new file and you dont commit or stash that change and switch, you wont get error and that file will be visible in the switched brach as well.

- git branch -d  <branch-name> // cannot delete the branch you switched in
- git branch -m <branch-name>// you need to be switched in the branch you want to rename

- git switch - // takes you to branch you were on

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

HEAD normally points to the branch pointer that points to last commit

- git checkout <commit> // detach head warning - jumped back in time
  - When we checkout to partcular commit, HEAD points at that commit rather than at branch pointer.
    - Examine the contents of old commit
- git switch master //Leave and go back to wherever you were before.

- After moving back to some commit you can create a branch from that commit and do things differently if you like.
 
- git checkout HEAD~1 // referencing previous commits relative to a particular commit. HEAD~1 previous commit

- git checkout HEAD <filename.ext> <file2> ..|| git checkout -- <filename.ext> // undo the new changes made to that file and revert back to the HEAD
- git restore <file1>// does the same thing of reverting back to HEAD as default source
  - git restore --source HEAD~1 <file1> // will restore the file state(content) from the commit prior to HEAD, you can also use particular commit hash
  - git restore changes the commit state of file and doesn't move HEAD.
  - git restore --staged <file> // unstage the staged file.

- git reset <commit-hash> // Actually moves the branch pointer backwards, eliminating commits. to undo commits, reset the repo back to a specific commit but the changes are still there as unstashed changes, other branches will have those commits
  - git reset --hard <commit> || git reset --hard HEAD~1 // removes commits as well as the changes in your files, other branches will have those commits
 
- git revert <commit> // creates a brand new commit which reverses/undos the changes from a commit. Because it results in a new commit.

- NOTE: using revert is better in collaboration environment as we want the removed commit to be part of the commit history instead of removing it but at your local branch you can just reset because we dont want the commit history and remove the commit completely. Basically, If you want to reverse some commits that other people already have on their machines, you can use revert.

## rebasing (avoid merge commits) - rewrite history
- alternative to merging
  - git switch feature
  - git rebase master
 
  - NOTE: Never rebase commits that have been shared with others. If you have already pushed commits up to Github...Do not rebase them unless you are positive no one on the team is using those commits. don't rebase the master branch, you can rebase your work(feature branch) 

  - merge conflict in rebase
    - if you can resolve git add those files and git rebase --continue
    - else git rebase --abort
- as a cleanup tool (Interactive rebase) // cleanup commits in the branch you are currently in, do with branch that is currently with you and not with other contributors.
  - git rebase -i HEAD~4 // rebase the branch you are on, rebasing changes the hash of the commits
  - reword // change the commit message
  - squash/ fixup // squashing 2 commits into 1 (previous and the one you have marked)
  - drop // completely removes commit, with the thing you pushed in it.
 
## Git tags(mark version, releases)
- git tag
  - git tag -l "*beta*"
- git checkout <tag-name>
- git diff <tag1> <tag2>
- git tag <tagname> // lightweight
- git tag -a <tagname> // annoated tag contains more information
- git show <tagname>
- git tag <tagname> <commit> // tagging earlier commit
- git tag -f <tagname> // moving already existing tagname
- git tag -d <tagname> // deleting a tag
- git push --tags || git push origin tagname// pushing tags to remote repo by default tags are not pushed to remote repo

## reflogs

- git keeps a record of when the tips of branches and other references were updated in the repo. reflogs are only for local repository. old entries are removed in 90 days.
- .git -> logs -> head
- git reflog show HEAD
- name@{qualifier}
- git reflog <branchname>@

## git aliases
[alias] s= status l = log cm = commit -m a= add
- In config file [alias] s=status
- git config --global alias.showmebranches branch
- git cm "first commit"
  
### Useful aliases
- 

## Config file
- local(.git -> config) and global
- cat ~/.gitconfig 

## Github

- [Github Setup SSH Config](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- git clone <repo-url> // always check you are not in a repository it creates a new folder

### Git remotes connecting to github

- git remote
- git remote -v
- git remote add origin <url> // origin can be changed to something else, origin is just a convention.
  - git remote rename <old> <new>
  - git remote remove <name>
- git branch -M main // renaming master to main
- git push -u origin main // -u sets the upstream of the local main branch so that it tracks the master branch on the origin repo
- git push <remote> <local-branch>:<remote-branch> 
  - git push origin cats:master


### Fetching and Pull

- git branch -r // shows remote branches
- git checkout origin/main
- git checkout main

- connecting remote to local branches
    - we can just create a branch named same as remote one
    - git switch <remote-branch-name> || git checkout --track <remote>/<remote-branch-name>

- Fetch
  - git fetch <remote> // updates the remote tracking branch with the latest changes from the remote repo.

- Pull
  - git pull <remote> <branch>// updates working directory with the remote changes+
 
git pull = git fetch + git merge

### Adding collaborators
### Github gists
### Github pages
- static webpages(portfolio site, documentation)




## Collaboration Workflow

### Centralized workflow
- everybody working on same branch

### feature branch workflow
- nobody works on master branch, all development is done on feature branches

#### Pull requests
  - do some work locally on feature branch
  - push feature branch to github
  - open a pull request using the feature branch just pushed to github.
  - wait for PR to be approved and merged

### Configuring Branch protection rule
add rule
  - main
  - require pull request reviews before merging

### Forking (make copy of repo on your github) - making contribution to open source
- If not collaborator, enables anybody to do contributions
  - Fork the project
  - clone the fork
  - add upstream remote // to stay upto date from original repo // only take pull from upstream dont push to it, because you dont have collaborator privileges.
  - do some work // creating separate branch
  - push to origin
  - open PR
  
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

## Git Behind the Scenes

- uses SHA1 determenistic // returns 40 digit hexa, 2 initial character makes the directory name and rest 38 make the file name in objects folder
.git -> config // local configuration
.git -> ref -> heads // there would be as many files as there are branch and each file will have head of that branch., same for remotes dir.
HEAD file -> current head
.git -> objects // Core of git, all content and commits live here (hashing,  blobs, trees)
- git hash-object <file>
- echo 'hello' | git hash-object --stdin
- echo 'hello' | git hash-object --stdin -w //store it in object
- git hash-object <file> -w

- git cat-file -p <object-hash>// retrieving data out
- git cat-file -p <object-hash> > <file> //retrieve and store it in some file
- git cat-file -t <hash> // gives type of hash

- object type Git
  - annotation
  - trees store the content of a directory. Each tree contains pointers that can refer to blobs and to other trees. Each entry in tree contains the SHA-1 hash of a blob or tree, as well as the mode, type and filename
    - git cat-file -p master^{tree}
    - type hash file-name
  - blobs are object type Git uses to store the contents of files in given repo. They just store content of the file, not even the filename.
  - commits combine a tree object along with information about the context that led to the current tree. Commits store a reference to parent commit(s), the author, the commiter and commit message
    - tree
    - parent
    - author
    - commiter
    - message
