---
layout: post
title:  Git
date:   2019-10-20 13:01:47 -0500
categories: study git
---

### ARCHIVE 
- EXPORT a project at a commit-point zip-file from - `git archive --output="<path/to/output/filname.zip>" --format="zip" --verbose <commit>`
  - For ex. `git archive --output="C:/Users/me/GitOutputs/HEAD.zip" --format="zip" --verbose HEAD`

### BRANCH
- LIST all branches - `git branch -a`
- LIST only remote-branches - `git branch -r`
- DELETE a local branch - `git branch -D <branchname>`

### CHECKOUT
- CHECKOUT branch and set upstream - `git checkout -b <new/branch/name> <remotes/branch/name> --
- CHECKOUT only particular file from stash - `git checkout 'stash@{N}' <path/to/file>`
  - For ex. `git checkout 'stash@{1} README.md`
- CHECKOUT an orphan branch - `git checkout --orphan <temp/branch/name>`
- CHECKOUT few files from a different branch - `git checkout <different-branch> -- <file1> <file2>` :star:

### CLONE
- CLONE a single-branch - `git clone <url> <name> -b <branch> --single-branch`

### CONFIG
- VIEW all config as a file  - `cat ~/.gitconfig` or `notepad++.exe ~/.gitconfig`
- VIEW all config with git command - `git config --list`
- SET config - `git config <configParameterKey> <configValue>` - For ex. `git config core.sparseCheckout true`

### COMMIT
- COMMIT an empty diff - `git commit --allow-empty -m <message>`

### DIFF
- VIEW difference of a file in working-tree with another commit - `git diff <commitID> -- <file/path>`
  - For ex. `git diff HEAD -- package.json`
- VIEW difference of a file between two commits - `git diff [options] <commitID1> <commitID2> -- <path/to/file>`
- VIEW difference with `summary` and `stat` - `git diff --stat --summary <id1> [<id2>]`
- VIEW only name of files as diff - `git diff --name-only HEAD`.  [More here](https://stackoverflow.com/questions/1552340/how-to-list-only-the-file-names-that-changed-between-two-commits)

### FETCH
- FETCH a branch from remote - `git fetch <origin> <branch>`

### LOG
- LOG out previous commits - `git log --pretty=format:"%h - %s"`
  - More details about formatting here : [Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)


### PUSH
- PUSH to a remote with different name: `git push <origin> HEAD:<remote-branch-name>`
  - For ex. `git push pinned-origin HEAD:master`
- DELETE a remote-branch - `git push <origin> --delete <branch/name>`
- DELETE multiple remote branches - `git push --delete <origin> [branch1, branch2,...]`

### PULL
- PULL branches with unrelated histories: `git pull <origin> <remote/branch> --allow-unrelated-histories`
  - ex. `git pull origin master --allow-unrelated-histories`

### REMOTE
- SHOW all remote repository info: `git remote show <origin>`

### RESET
- RESET to a commit-id and discard(permanently delete) all changes - `git reset [commidID] --hard`
- RESET to a commit-id and unstage all changes - `git reset [commitID] --mixed`
- RESET to a commit-id and keep all stage all changes - `git reset [commitID] --soft`

### STASH
- STASH changes - `git stash push --all -m "<message>" --`

### SHOW-REF
- SHOW all references - `git show-ref`
 
### STATUS
- GET status with `no untracked-files` - `git status -uno` 

### UPDATE-INDEX
  - EXCLUDE files in `add` and `commit` - `git update-index --assume-unchanged <path/to/file>`
    - For ex. `git update-index --assume-unchanged package.json`
  - REVERT excluded to be included in `add` and `commit` - `git update-index --no-assume-unchanged <path/to/file>`

### UPDATE-REF
  - DELETE a `ref` - `git update-ref -d -- <ref1> <ref2>...` (`git show-ref` to get a list of all `refs`)
 
## How to...?
  - CLONE a particular-sub-folder from a particular-branch:
    - INITIALIZE `git` in a folder - `git init`
    - ADD remote origin with: `git remote add origin <path/to/origin.git>` 
    - SET the config to allow `sparse-chekouts` - `git config sparseChekout true`
    - CREATE a `sparse-checkout` folder under `.git/info/sparse-chekout` and add the path to the particular folder
      - `touch .git/info/sparse-checkout` and edit the `sparse-checkhout` file to include the `path/sub-directory`
      - For ex. `packages/react-scripts` OR 
      - Single line command:
        - with `Bash` - `echo "path/to/sub-directory" >> .git/info/sparse-checkout`
        - with `Powershell` - `Set-Content .git\info\sparse-checkout "some/sub-folder/you/want/*" -Encoding Ascii`
      - PULL the branch we want: `git pull origin <branch>` for ex: `git pull origin master`
  - ADD and COMMIT all files except a few:
    - ADD all files to begin with : `git add .`
    - RESET the files that we don't want in the commit: `git reset -- path/to/file1 path/to/file2`
  - FETCH a single-branch from the remote-repo:
    - FETCH the branch - `git fetch <remote> <branch/name>`
    - FETCH head of that branch - `git branch <branch/name> FETCH_HEAD`
    - CHECKOUT that branch - `git checkout <branch/name>`
    - MERGE remote-head - `get merge FETCH_HEAD`
    - MERGE remote-head without verification - `git merge FETCH_HEAD --no-verify`  :)
  - DELETE a branch that doesn't appear on remote: 
    - [Reference Link](https://stackoverflow.com/questions/9378760/git-push-local-branch-with-same-name-as-remote-tag)
    - Error message is something like `dst refspec poc/eslint-react matches more than one`
    - TRY this `git push --delete refs/poc/eslint-react`
  - DIFF between a local-branch and remote-branch
    - FETCH the remote-branch `git fetch <origin> <branch>`
      - This will create a FETCH_HEAD branch which has the remote branch on it.
    - CHECK diff with summary - `git diff --summary FETCH_HEAD` - This will display the diff of FETCH_HEAD with current-branch 
    
### What is the difference between `FETCH` and `PULL`? What is `FETCH_HEAD`?
FETCH | MERGE
------|-------
**FETCH** will only *fetch* the branch from specified origin | **PULL** will *pull* the remote-branch into the current branch - i.e. it will *`FETCH` + `MERGE`*
**FETCH** will provide the *fetched-branch* on a **FETCH_HEAD** branch | **PULL** too provides a **FETCH_HEAD** if the corresponding remote branch is not available.  We can then doe a `git branch <branch> FETCH_HEAD` which will create a new branch from `FETCH_HEAD`.  Next we can chekout that branch with `git checkout <that-branch>`.

