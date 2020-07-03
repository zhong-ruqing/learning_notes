# Useful Resources

- video tutorial for beginners: <https://www.youtube.com/playlist?list=PL4cUxeGkcC9goXbgTDQ0n_4TBzOO0ocPR>
- official video channel: <https://www.youtube.com/githubguides>
- recommend IDE: [Atom](https://atom.io/)
- recommend console for windows: [cmder](https://cmder.net/) (full version has git pre-installed)
- install git: [git](https://git-scm.com/)
- git documentation: <https://git-scm.com/doc>
- official github guide: <https://guides.github.com/>

# Git

Git is a version control system

- `git --version` (to check the git version on your computer)

## Config

more detail in git documentation: [git-config](https://git-scm.com/docs/git-config)

- `git config --list` (to see all the configuration settings, such as user name and user email)
- `git config --global user.name <yourusername>` (to set your user name)
- `git config user.name` (to show the user name)
- `git config --global user.email <youremail>` (to set your user email address)

## Creating a Repository

Steps:

- go to the folder that you want to create the repository
- open "cmder" or "GitBash"
- type the command `git init`
- a hidden folder with name ".git" will show in the root folder

PS: You can create a repository either in an empty folder or in an folder with existing files.

## Staging Files

![image-20200611143349246](E:\notes\git_github_tutorial.assets\image-20200611143349246.png)

The modified files in the repository need to be put in staging area first, then can be committed.

- `git status` can show which files have been changed as well as which files are in the staging area, the tracked files are green, the untracked are red
- `git add <file>` can add the changed file in the staging area
- `git add .` can add every modified file in the staging area
- `git rm --cached <file>...` can remove the file that we don't want to commit from the staging area 

PS: The meaning of staging is to separate the commits for separate changes, which makes our work more clear.

## Making Commits

After adding the wanted modified files in the staging area, we can do commit.

- `git commit -m "description about this commit"` (the description need to be descriptive and clear, because you will use that as reference in the future)

- `git log` can show the commit history
- `git log --oneline` can show the condensed commit history

## Undoing Stuff

![image-20200611181138684](E:\notes\git_github_tutorial.assets\image-20200611181138684.png)

### checkout commit

read-only, checkout will not alter the commit history

- `git log --oneline` can let you view all the commit history and see which commit you want check, find the ID of it
- `git checkout <IDOfCommit>` can let you detach the head of master branch, check the code state of a particular commit
- `git checkout master` can let you reattach the head of master branch

### revert commit

undo one particular commit, will add a commit which shows "revert "the particular commit""

- `git log --oneline` to show the commit history and find the ID of the commit that you want to revert
- `git revert <IDOfCommit>` to revert the particular commit

### reset commit

danger, will set the commit history back to one particular commit state permanently

- `git log --oneline` to show the commit history and find the ID of the commit state that you want to go back permanently
- `git reset <IDOfCommit>` to reset the commit history back to one particular commit state,  but everything you have done after that commit will not be deleted, just be uncommitted

- `git reset <IDOfCommit> --hard` to reset the commit history back to one particular commit state, everything you have done after that commit **will all be deleted**

## Creating Branches

![image-20200611184454006](E:\notes\git_github_tutorial.assets\image-20200611184454006.png)

The feature branch will not affect the master branch. You can use it to test new features, if you like it, you can merge it with the master branch, if you delete it, the master branch will still be stable. You can also work in team, you and you teammate can work on different feature branches.

- `git branch <BranchName>` to create a new feature branch

- `git branch -a` to show all the branches, the active branch will be green with a (*) mark

- `git checkout <BranchName>` to switch to particular branch
- `git checkout -b <BranchName>` to create a new branch and switch to this new branch

## Deleting Branches

- make sure you are in the master branch now, if not, use `git checkout master`
- `git branch -D <BranchName>` to delete the branch that is not fully merged with master branch
- `git branch -d <BranchName>` to delete the branch that is fully merged with master branch

## Merging Branches

- make sure you are in the master branch now, if not, use `git checkout master`
- `git branch -a` to check all the branches, find the branch that you want to merge
- `git merge <BranchName>` to merge the feature branch with master branch

### Conflicts

If you tried the mentioned steps to merge the branches, but conflicts happens, the merge will not success automatically, then you need to do the following things:

- you need to change the file manually, then `git add .` and `git commit` (with out -m to write message)
- if the text editor opens, then use <kbd>Shift</kbd> + <kbd> : </kbd>, type "wq" and <kbd>enter</kbd>to exist the editor without doing other things. 
- After that, check the commit history with `git log --oneline`, you can see that the branch merging has been successfully down.

# GitHub

## Intro

![image-20200611193040228](E:\notes\git_github_tutorial.assets\image-20200611193040228.png)

### Push an Existing Local Repo to GitHub

- create a new repo in GitHub (don't need to initialize a README file)
- get the URL of the remote repo, go to local repo
- `git status` to make sure the commit has been done and nothing has been left
- `git push <URLOfTheRemoteRepo> <BranchToPush>` to push to local repo to the remote repo

After we have pushed the local repo to the remote repo , if we have done some changes and want to push that again, and we don't want to type the URL every time:

- `git remote add <AliasOfTheRemoteRepo> <URLOfTheRemoteRepo>` to give an alias (usually "origin" is used as default alias) to the remote repo, then we can just use the alias to do the push

- `git push <AliasOfTheRemoteRepo> <BranchToPush>` to easily push the commits of the local repo to the remote repo

### Create a New Repo in GitHub from Scratch and Clone it

- create a new repo in GitHub with initializing a README file (so when clone it, everything will be in sync)
- get the URL of the remote repo, go to local folder
- `git clone <URLOfTheRemoteRepo>` to clone the remote repo in current folder to get the local repo

- we don't need to give the URL of the remote repo an alias because it was already done when we clone it, use `git remote -v` to check the alias of the URL (default alias is "origin")
- `git push <AliasOfTheRemoteRepo> <BranchToPush>` to push the commits from local to remote repo

## Collaborating on GitHub

- switch to the master branch, use  `git pull <AliasOfTheRemoteRepo> <BranchToPull>` to pull the codes from the remote repo to update the local repo, in this case the "\<BranchToPull\>" is "master"
- `git checkout -b <NameOfFeatureBranch>` to create a new feature branch so that the master branch is not messed up
- work in the feature branch, don't merge the feature branch with master branch locally because the team members need to check the code in the feature branch first, instead, push the feature branch to the remote repo using `git push <AliasOfTheRemoteRepo> <NameOfFeatureBranch>` 
- go to GitHub to check the remote repo, by clicking <kbd>Compare and pull request</kbd> button, you can go to the process to merge this new feature branch with master branch in the remote repo, meanwhile, the team members can command be seen
- if the comments is asking you to change something, go to local repo, then finish the changes in the local repo, then type `git add .` and `git commit -m “description about the changes”` to finish the commit in local repo, after that, use `git push <AliasOfTheRemoteRepo> <NameOfFeatureBranch>` to update the feature branch in remote repo
- after merging is completed, the feature branch can be deleted safely (you don't need to delete it)

## Forking and Contributing

Forking is to clone a repo from other's account to your own account, after that, you can make changes in the repo on your own account, clone it to the local, do the changes, commit, and push to the remote repo, but you cannot merge this repo to the holder of this original repo, but you can start a request, if the holder is satisfied, then the holder can do the merging.

.