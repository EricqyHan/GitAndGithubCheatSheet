# GitCheatSheet

**Github Bootcamp: Colt Steele**

## Section 5: Commits In Detail and Related Topics

Note to set VS Code as Default Editor:

[Git Setup Link](https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config)
[Git Lab Setup Link](https://docs.gitlab.com/ee/ssh/#add-an-ssh-key-to-your-gitlab-account)

_A3.1 Appendix C: Git Commands - Setup and Config_
To use VIM as editor
`git config --global core.editor "vim"`

To use VS Code as editor
`git config --global core.editor "code --wait"`

**Escaping Vim in Terminal/Using Vim in terminal**

1. Hit `i` key.

- This will let you insert your commit message

2. Hit `esc` key to leave insert mode
3. Type in `:wq`

- W stands for write
- Q stands for quit

4. Your commit will be pushed

Note to use Git Status to check on what needs to be pushed
_Hit `q` key to exit Git Log_

- Note that the commit hashes is how we revisit a commit, undo a commit, or check out a commit
- `git log --abbrev-commit`
- `git log --oneline` cuts log down to oneline

**How to use Git Kraken**

1. Open up file you want to view/commit with
2. You can see what files are not commited
3. Once you stage a file you can use the terminal to see the status with `git status`. Note that stage is the same as `git add`
4. Add a commit message and then hit stage files/changes to commit

**Fixing Commits with Amends**
_Amends allows us to redo the previous commit using the --amend option_
`git add` add the missing file you forgot to add to the previous commit
`git commit --amend`
From here you can either edit the commit message or close/exit the editor and your last commit will be "updated"

**Ignoring Files**
We want this to ignore API keys, credentials, app secrets

- On mac .DS_Store files. These files are just system hidden files. Also don't want to upload dependencies

Create a .gitignore file in your root directory
Inside we can write patterns to tell Git which tiles and folders to ignore

- .DS_Store will ignore files name .DS_Store
- folderName/ will ignore an entire directory
- _.log will ignore and file with the .log extension. Note: that _ is the wildcard
- when you run Git Status you won't see the .DS_Store or other files that you don't want to commit anymore
  [https://www.toptal.com/developers/gitignore](Git Ignore recommendation list)

## Section 6: Git Branching

Note that we always start on master

**HEAD** is current location we are currently checking out.

- Is simply a pointer that refers to the current "Location" in your repository. It points to a particular branch reference.

- So far, head always points to the latest commit you made on master branch, but soon we'll see that we can move around and HEAD will change.

**Viewing Branches**
`git branch` - will show you branches you have

- to get out just type `q`
  `git branch <branch name>` - no spaces in branch name
  example branch
  `git branch bugfix` - new branch called bugfix will be created
- To switch branch type in `git switch <branch name>`
- `git switch bugfix`
- You can now make edits to your new branch
- Switch back to _Master_ branch and your edits won't be there

**Short version of git add git commit**

- `git commit -a -m`

**Creating a branch and switching to it**

- `git switch -c <branch name>`
  example `git switch -c newbranchname`

**Switching Branches with unsaved changes**
You will have to commit your changes or stash them before switching branches

**Deleting or renaming branches**
`git branch -d <branch name>`
Example
`git branch -d deleteMe`
or
`git branch -D deleteMe` to force it if you haven't merged it yet

**Rename A Branch**

- Switch to branch you want to rename
- rename with `git branch -m <branch new name>`
- example: `git branch -m 2000s`

## Section 7: Merging Branches

Merging - Makes it super easy to work within self-contained cntexts, but often we want to incorporate changes from one branch into another.

Note that we merge branches, not specific commits. We always merge to the current HEAD branch

`git branch -v`

- get last commits and versions

To merge you have to swtich to the branch you are trying to merge into

- Note that the branch you merged from is still there

**Merge Conflicts**
Make a new branch for two branches you want to merge

- merge into one branch

**Fast Forward Merge**

- With a fast forward merge, we don't touch master again
- we can add as many commits in current branch as we want, but we don't change master in the meantime
- So all master has to do is catch up with current branch
- make your edits in current branch and then switch to master with you are ready
- then `git merge <branch you were working on and want to merge>`
- Master is now up to date

**Merge No Conflict**
No conflict in this merge or fast-forward because Master has a new file and does not conflict with new branch

**Merge with conflicts**
Pick what updates you want to add in VS code

## Section 8: Comparing Changes With Git Diff

Git diff - Without additional options, git diff lists all the changes in our working directory that are not staged for the next commit

**Chunk Headers**
@@ -3,4 +3,5 @@ orange

example
file a
`red orange yellow green blue purple`

file b
`red orange yellow green blue indigo vilot `
Chunk is telling us we get four lines from line 3 starting from _yellow_.

- In file a, we see three colors after yellow (including yellow makes four)
- In file b, we see four colors after yellow (including yellow makes five)

**git diff**
`git diff`

- will show all the changes in our working directory that are NOT staged for the next commit

**git diff head**
`git diff head`

- list all changes in the working tree since your last commit.

**git diff --staged or --cached**
Note: git diff --staged and git diff --cached are the same

- will list the changes between the staging area and out last commit
- "show me what will be included in my commit if I run git comit right now"
  `git diff --staged`
  `git diff --cached`

**git diff-ing specific files**
We can view the changes within a specific file by providing git diff with a filename
`git diff -staged <filename>`

**Comparing Branches**
`Git diff branch1..branch2`
or
`Git diff branch1 branch2`

- git diff branch1..branch2 will list the changes between the tips of branch1 and branch2

**Comparing Commits**
`git diff commit1..commit1`

- to compare two commits, provide git diff with the commit hashes of the commit in question

## Section 9 - Git Stash

Git provides an easy way of stashing these uncommitted changes so that we can return to them later, without having to make unnecessary commits
`git stash`

- will take all uncomitted changes and stash them, so we don't see them anymore but we can go back and get them later

`git stash pop`

- use git stash pop to remote the most recently stashed changes in your stash and reapply them to your working copy

`git stash apply`

- you can use git stash apply to apply whatever is stashed away, without removing it from thje stash. This can be useful if you want to apply stashed changes to multiple branches.
- comes in handy if you need to apply changes accross multiple

`stashing multiple times`

- you can add multiple stashes onto the stack of stashes. They will all be stashed in the order you added them.

`git stash list`

- can see all of your stashes
- if you do `git stash pop` you will see your most recent git stash
- you can reference particular stashes by referencing specific stashes
  `git stash apply stash@{2}`
- pick the stash you want

note: if you picked the wrong stash you can revert by deleting the changes or running `git checkout -f` to remove any non-commited changes

- Most recent stash will be stash@{0}

**Dropping stashes**
To deletre a particular stash, you can use `git stash drop <stash-id>`

**Completely empty out stashes**
Use `git stash clear`

## Section 10: Undoing Changes and Time Traveling

**Git Checkout**

- git checkout is like the Git Swiss army knife. We can use git checkout to create branches, switch to a new branch, restore files, and undo history.

`git checkout <branch id>`

**Detached Head**
When we checkout a particular commit, HEAD points at that commit rather than at the branch pointer.

**Referencing commits relative to HEAD**
`git checkout HEAD~1`

- Note you would use HEAD~2 or HEAD~3 for hashes down the line
  - Basically HEAD~`1 goes back one comit and HEAD~2 goes back 2 and so on

Use `git switch -` to get back to where you were before the `git checkout HEAD~1` command

**Discard Changes from a file**
`git checkout head`

or
`git checkout --<filename>`

**Git Restore**

- to restore changes done to a file.
  `git restore <filename>`
- or
- `git checkout head <filename>`

**Unmodifying Files with Restore**
`git restore --source HEAD~1 <filename>` will restore the contents of <filename> to its state from the commit prior to head. You can also use a particular commit hash as the source.

**Unstaging files with restore**

- We can unstage files using `git restore --staged <file-name>`
  this will remove anything we have staged by accident (api keys, .gitignore, etc)
- note that git will tell you what to do. If you stage one file alone it will tell you how to unstage it if you type in `git status`

**Git Reset**

- resetting the repository back to a specific commit. The commits are gone.
  `git reset <hash>`
  - commits will be gone but changes will still be in repo. This git history stops after the git reset.
  - Now we switch to a new branch and bring changes over to new branch
    `git switch -c newbadbranch`
  - add and commit changes
  - switch back to master and "bad changes" won't be there anymore

**Reset --hard**

- will delete the last commit and associated changes
  `git reset --hard <commit hash>`

## Section 11: Github

**Viewing Remote**

- To view any existing remotes for yhou repository, we can run `git remote` or `git remote -v`
- This just displays a list of remotes. If you haven't added any remotes yet, you won't see anything

**ADDING A NEW REMOTE**
`git remote add <name> <url>`
example: `git remote add origin https://github.com/blah/repo.git`

Note: Origin is a conventional Git remote name, but it is not at all special. It's just a name for a URL.

When we clone a github repo, teh default remote namesetup for us is called origin. You can change it. Most people leave it.

We can rename and delete remotes
`git remote rename <old><new>`
`git remote remove <name>`

**The -u option**

- stands for upstream of branch we're pushing. Think of it as a link connecting our local branch to a branchb on GitHub.
  `git push -u origin master`

## Section 13: Github Grab Bag - Odd And Ends

**Gists**

## Section 14: Fetching and Pulling

**Remote Tracking Branches**

- Origin/master references the state of the master branch on the remote repo named origin
- Upstream/logoRedesign references the state of teh logoRedesign branch on the remote named upstream (a common remote name)

- Note that when you have a branch **master** branch you are workin on and make commits to it, you will be ahead of **origin/master** by one or more commits.
  - To see what the project looked like before you made your commits you will have to have to checkout these remote branches with `git checkout origin/master`
  - origin/main is remote tracking branch
- Switch to `git checkout origin/main` and you will be in detached head
- This is a reference to where the main branch **WAS**
- Switch back to the main branch with `git switch main`

  **Working with Remote Branchs**

- To see remote branches you will have check for the remote branches with `git branch -r` and then `git checkout origin/"branch name"`
  **OR**
- We can just change branches that exist online with `git switch <branch name>`

**Git Fetch**
Fetching - Allows us to download changes from a remote repo, but those changes will not be automatically integrated into our working files.

- Please get the latest info from github, but don't screw up my working directory
  `git fetch origin`
- or just fetch one branch
- `git fetch <remote><branch>`
