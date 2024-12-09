# **Git and Version Control**  

// research about packing  

## Version Control  

What is version control? Version control deals with managing changes in files over time. It keeps tracks of drafts, revisions, and edits we make.  

> Benefits of using version control:  
> - Collaboration: Multiple developers can work concurrently on a single project.  
> - History tracking: details of every modification; when, who, and why.  
> - Rollback: easy go to previous versions.  
> - Branching: parallel development of features.  
> - Backup: Robust system to safeguard project's history.  

### History of Version Control  

**Manual Method**: Copying files with different names.  
- cons: error-prone, difficult to manage, space inefficient.  
**Local Version Control Systems (LVCS)**: Revision Control System (RCS)  
- early attempts to automate version control.  
- files stored locally.  
- kept patch sets (diff between files) in special format on disk.  
- Operates on a single file -> "checked out" modifying a file, "checked in" everyone else can use.  
- only one user can edit a file at a time.  
**Centralized Version Control Systems**:  
- One global repository: every user commits to reflect one's changes in the repository.  
- Others see changes by updating.  
- Still used in some research labs.  
- Pros: collaboration, see how much everyone is doing, admins can control who can do what.  
- Cons: single point of failure, limited offline access, performance issues.  

## Intro to Git 

#### Architecture  

A global repository on a server, and each user has an individual repository and a working copy.  

- Commits reflect changes in the local repository.  
- Need to push to make visible on central repository.  
- Pull changes into local repository.  

![distributed-version-control-diagram](https://miro.medium.com/v2/resize:fit:1400/1*V816gsIRgzJPd-5wGvQgIQ.png "Distributed Version Control System Diagram")  

![git-version-control-diagram](https://bestia.io/assets/images/git/git01.png)  

**Pros:**  
- Robust: Multiple backups. every developers local repo is a full backup, reducing the risk of data loss.  
- Offline work: Fully functional offline: commit, branch, merge, view history, etc...  
- Speed and Performance: Most operations are local. Committing, branching, merging.  
- Flexible branching/merging: Creating and switching between branches is quick and efficient.  
- Advanced merging: sophisticated tools for resolving merge conflicts.  
- Collaboration: multiple workflows: share changes directly, or through central server. Code review through pull/merge requests.  

**Cons:**  
- Steeper learning curve: more complex concepts, various workflows.  
- larger storage requirements: full local repository. Esp for large projects.  
- Not ideal for large binary files. Generally not efficient at managing large binary assets (ie. game dev).  
- Complexity in managing multiple remotes: synchronizing work with several depositories.  

#### Key Git Concepts  

**Repository:** Central storage for versions of a project's files.  
**Commit:** Snapshot of project at specific time. Captures changes and includes description message.  
**Branch:** Parallel versions of the project. Allow us to work on different features or bug fixes without affecting the main codebase.  
**Merge:** Combine changes from one commit/branch to another.  
**Checkout:** Switch between branches/commits or restore files to a specific versoin.  
**Pull:** Fetch and merge changes from remote repository into local branch.  
**Push:** Upload local commits to remote repository.  
**Tracked:** Git is aware of tracked files. Everything you `git add` will become tracked.  
- Types of tracked files: unmodified (file hasn't changed since last commit), modified (file chnaged, but unstaged), staged (file in staging area, index).  
**Staging Area:** Also called index. Holds changes you want to include in next commit.  
**Working Directory:** where you make changes. A single checkout of one version of the project.  

## Git's Internals  

The `.git` directory is where git stores data.  

### Structure  

 Object files are the core storage of git's data. Indexed via a 40-character hexidecimal SHA-1 hash.  

**Blobs**: represents content of individual files.  
- Each version of a file is stored as a different blob.  
- Doesn't store metadata, just the content. SHA-1 hash is the name of the blob.  
- `git show HASH` Show blob corresponding to hash.  
- `git hash-object FILE` Shows hash corresponding to file.  

**Trees**: represent directory structure of your project at a specific point of time. Links blobs together. Like a folder.  
- contains hashes of sub-trees and blobs, along with the parent.  

**Commits/Snapshots**: represents snapshot of project's history. 
- Contains: (1) pointer to a tree, (2) info about author and commit message, (3) pointers to parent commits. (Forms commit history graph, the DAG).  
- Git saves space by using pointers -> if nothing changes don't have to store anything new.  
- Each object has a unique Hash 

	~COMMIT EXAMPLE~
	tree e4f5g6h7...
	author John Doe <john.doe@example.com> 1678886400 +0000
	committer John Doe <john.doe@example.com> 1678886400 +0000
	parent abcdbsh34...
	message some commit message

> The graph of commits, the commit history graph, forms a DAG (Directed Acyclic Graph).  
> Commits are directionally related and don't form a directional closed loop.  

**packfiles** Git sometimes packs several objects into a single binary.  
- Automatically happens when: loose objects, pushing to remote surver, running `git gc`  


### Internals  

**HEAD:** A symbolic name (link) to the currently checked out commit (current index).  
- Always points to most recent commit.  
- Usually points a branch name.  
- Detaching HEAD -> attach the head to a commit instead of a branch.  

**config:** Contains repo-specific config information.  

**refs/:** Contains all reference pointers to commits: heads, remotes, tags, branches.  
- heads: Folder that contains, for every branch, where the head is. Stored as SHA-1 hashes.  
- remotes: Folder containing remote repositories.  
- tags: tags are tied to a commit.  
- There also exists a packed version of refs/ called packed-refs.  

**hooks/:** For automation. Can create scripts that run whenever a commit, merge, patch, etc... occurs.  

**objects/:** Where the bulk of stuff is stored! Holds all object files.  
- Files are stored in subdirectories for performance -> 256 subdirectories indexed from 00 to ff.  
- Objects include: commits, trees, blobs (files).  
- An object is stored in the subdirectory corresponding to the first 2 characters of their hash.  
- Use `git cat-file -p HASH` to see the internals of an object file.  

> a SHA-1 hash `a1b2c3d4...` would be stored in `.git/objectws/a1` with filename `b2c3d4...`  

#### Relative References  

Can specify commits with a relative reference instead of with hash number.  
- `^` One commit up. Defaults to the first parent of the commit.  
- `^n` One commit up to the nth parent.  
- `~n` Move n commits up the tree.  

## Git Commands  

`git help <command>` Get help on a Git command.  

### Local Changes  

#### Local Repository Manipulation

**`git init`** Creates new repository tracking the current directory.  
- creates a `.git` directory to track the current directory.  
- `-b` to rename the master branch.  

**`git add FILE`** Stages current changes to file. (Add file to index).  
 - `.` Add all files.  
 - `-A` Add all files as well.  
 - `LICENSE`  

**`git commit`** Commits staged changes.  
- `-m "MESSAGE"` to add a commit message from command line.  
- `-a` Automatically stage all tracked files and commit.  
- `--amend` Allows you to stage changes and amend to last commit.  

**`git rm`** Untracks a file that is already checked in, and removes it from the working directory.  
- `-f` Force removal. Only if file was modified or already added to staging area.  
- `--cached` Untrack without removing from working tree.  

**`git checkout BRANCH`**  Switch working tree to a branch.  
- `--track REMOTE` Checkout a new branch that tracks a remote branch. Make sure to specify the remote repository, ie `origin/branch-name`.  

**`git tag "PATTERN"`** Tag points in repo history (ie. release points, etc.). Pattern is optional.  
- `-l` optional list flag.  
- `-a` annotated tags: stored as full objects. 
- `-m` Specify tagging message, stored with tag.  
- lightweight tags: Automatic if no specifying option. 'unchanging branch', points to specific commit.  
- `-d NAME` Delete a tag

**`git format-patch COMMIT`** Create patch files

#### Commits

**`git merge BRANCH`** Combine changes from BRANCH into current branch in a merge commit.  
- This commit has two parent commits, the two branches. Preserves history of both branches.  
- `-m "MESSAGE"` Include a message.  
- `--continue` Continue merge after resolving merge conflicts.  

**`git rebase BRANCH`** Also combines two branches like merge, but moves commits in current branch to the end of BRANCH.  
- Result: as if the changes in the current branch happened after the most recent commit in BRANCH. A linear history.  
- `-i` Interactive rebase. Review and edit commits during a rebase.  
  - Can reorder commits, `squash` (combine) commits, `edit` commit messages, `pick` specific commits.  

**`git restore FILE`** 
- `--staged` removes file from staging area, but keeps the changes in working directory.  

**`git reset COMMIT`** Reset to a previous commit.  
- Doesn't work in remote branches.  
- `--soft` Resets current branch to COMMIT, preserving changes in working directory and staging area.  
- `--hard` Rests working directory, staging area, and current branch to COMMIT. All changes since COMMIT are discarded.  

**`git revert`** Instead of removing a commit, appends a revised commit to the end.  d

**`git stash`** Temporarily save changes in working director and staging area to a "stash".  
- Used so you can work on something else or pull changes without conflicts.  
- Pushes changes to a stack-like structure, restoring a clean working directory.  
- `push -m FILE` Specify what to stash, with an optional description.  
- `pop` Applies changes from most recent stash to working directory, removing it from the stash.  
- `apply stash@{n}` Same as pop, but doesn't remove the stash from the stack. Specify the particular stash with `n`.  
- `list` Shows all stashes.  
	
**`git cherr-pick COMMIT1 COMMIT2`** Copy a commit to end of current branch (append after current head).  

### Displaying Info  

**`git status`** Status of changes: untracked, modified, staged.  
- `-s` or `--short` Simplified output.  

**`git branch`** shows branches being worked on locally.  
- `-d` Delete a branch.  
- `-m OLD NEW` Rename a branch.  
- `-a` List branches.  
- `-vv` List verbose info about local branches, including the remote repo each one tracks.  


**`git log`** Lists commits made in repository in reverse chronological order.  
- `-p` or `--patch` shows difference introduced in each commit.  
- `-<n>` Only show n number of previous entries.  
- `--stat` See abbreviated stats for each commit.  
- `--pretty=TYPE` Change log format: oneline, short, full, fuller, format (manually decide log format).  
- `--graph` Ascii graph showing branch and merge history.  
- `--since` for commits after specified date, or `--until` for commits before specified date.  

**`git diff`** Compares changes between commits, branches, working directory, staging area.  
- By default compares working directory with staged area.  
- `--staged` or `--cached` Compares staged changes to last commit.  
- `COMMIT..COMMIT` Compare two commits.  
- `BRANCH..BRANCH` Compare two branches.  
- `--text` Display as plain text.  

**`git cat-file HASH`** Show information about an object file.  
- `-p` Pretty print content. Automatically figures out the content type.  
- `-t` Display type of the object file. (commit, tree, file)  

**`git reflog`** Log of all git changes that have happened in the repository. Useful if you ever do anything crazy or anything goes wrong.  
- can reset to a previous state (`git reset --hard HASH`).  

### Working with Remotes  

**`git clone URL`** Creates local copy of remote project. Includes files, history, backups.  
- Creates a directory and initializes it.  

**`git remote`** Displays remote servers.  
- `-v` Shows more information about the remote servers.  
- `add SHORTNAME URL` Add a new remote repository.  
- `show REMOTE` Lists information about the remote server.  
- `rename OLD NEW` Rename a remote's shortname.  

**`git fetch REMOTE`** Pulls all changes from remote repo to local, without merging it with local repo.  
- `--all`
- `--prune` Remove remote-tracking references in local repository that no longer exist in remote repo.

**`git pull`** Automatically fetch from remote and merge with current branch.  

**`git push REMOTE_REPO`** Push the current branch to the remote branch it tracks in REMOTE_REPO. Only works if you are up to date with updates in remote.  
- can push a tagname as well, or use `--tags` option to transfer all tags.  
- `-u` or `--set-upstream` Establish a tracking relationship between a local and remote branch.  
- `-d` or `:REMOTE` Delete branch REMOTE from the remote repository.  

**Pull Requests**: Often will create rules where you can't push directly to remote main. Instead, push to a feature branch and create pull request to merge that branch with main.  

### Plumbing Commands  



### Debugging  

From lecture notes:  

> Scenario...  
> 1. You've discovered a bug in your project, bu the project worked correctly two weeks ago.  
> 3. Run `git bisect start`.  
> 4. Mark the current commit (where the bug is present) as bad: `git bisect bad`.  
> 5. Find a commit from two weeks ago using `git log` and mark it as good: `git bisect good <commit_hash>`.  
> 6. Git checks out a commit between those two points. Test for the bug.  
> - If the bug is present, run `git bisect bad`.  
> - Otherwise, run `git bisect good`.  
> 7. Repeat until Git identifies first bad commit.  
> Run `git bisect reset` to go back to original state.  
> `git bisect run` automates bisecting process by running a script or command.  
> `git bisect skip` Skip a commit if you can't test it or if test in inconclusive.  

#### Config  

**`git config`** set and get config variables.  
- 3 locations for config variables:
  - `[path]/etc/gitconfig`: Values applied to all users on the system. `--system`.  
  - `~/.gitconfig` or `~/.config/git/config`: Values specific to user. Affects all repositories in our system. `--global`.  
  - `./git/config`: Specific to single repository. Default config location. `--local`.  
- global values overwrite local values.  
- `--list --show-origin` Shows all settings and where they're coming from.  
- `user.name "NAME"` Sets user name.  
- `user.email email@gmail.com` Set email address.  
  - `core.editor NAME` Sets default text editor.  
- `init.defaultBranch NAME` Sets default branch name.  

**`.gitignore`** Files we don't want Git to automatically add.  
- Lines beginning with `#` are ignored.  
- Standard glob patterns work -> `*`, `[...]`, `?`.  
- Starting pattern with `/` avoides recursion.  
- Ending pattern with `/` specifies a directory.  
- Negate a pattern with `!`.  

Comprehensive list of commands can be found at [gitDocs](https://git-scm.com/docs "git commands documentation").  

### Good Git Practices  

1) Keep Main Clean: Don't commit directly to main branch, use feature branches for dev, create pull requests for review and integration.  

2) Fork the Repository: Allows you to work on individual copy of a repository without affecting the original.  

3) Maintain Branches: Keep branches organized. Use branches like dev for ongoing development, main for stable releases.  

4) Use descriptive commit messages: Explain purpose of the changes in the commit.  

5) Regularly pull updates: Keep local repository up to date. Ensures you're working with the latest codebase.  

6) Revert Bad Commits instead of Amending: if you make a mistake in a commit, avoid amending the commit history. Instead revert the bad commit with a new commit that undoes the changes.  

7) Use Gitignore: Create `.gitignore` file to specify untracked files. Prevents accidentally committing files.  

8) Review Pull Requests Thoroughly: Review changes made and provide constructive feedback. Maintains code quality.  

9) Document Changes: Document significant code changes, new features and fixes in project's documentation or README.  

10) Communicate Effectively: Git comments, pull request discussions, project management tools.  

What to not include in Git Repo:
- Sensitive info: passowrds, API keys, access tokens. Use environment variables or configuration files.  
- Large files: exclude large binary files (videos, images, compiled binaries).  
- Generated files: Exclude compiled code, logs, etc...  
- Dependencies: exclude dependencies. Use npm, pip, Maven, etc... to manage dependencies.  


## About Git

### What does Git do

Git Controls 3 things:  
1. working files (source code, current state of repository)  
2. history of project development. modeled with a tree of files  
3. index. "recording plans for the future".  


### Setting Up a Repository  

**Clone a remote repository** onto local environment  

> `git clone REMOTE-URL`  

OR: Create a local repository, and **link to a remote repository**. Make sure the remote repository is empty.

> `git init`  
> `git remote add origin REMOTE-URL`  

Verify that the remote repository was set correctly with  

> `git remote -v` //useful info!! 

Push changes in local repository to Github as follows, replacing master with the name of my default branch.  

> `git push -u origin master`  


### Adding files to a repository  

Stage the file for commit to your local repository.  

> `$ git add .`  
>  
> // Adds the file to your local repository and stages it for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.  

Commit the file that you've staged in your local repository.  

> `$ git commit -m "Add existing file"`  
>  
> // Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.  

Push the changes in your local repository to GitHub.com.  

> `$ git push origin YOUR_BRANCH`  
>  
> // Pushes the changes in your local repository up to the remote repository you specified as the origin  


### Good Commit Practices

When creating a commit message, include three parts: the subject line, body, and footer.

**subject line**: gives a summary of changes made. < 50 characters. Imperative ('Add this' not 'Added this'), specific and informative. Do not end with period.  

**body**: provides description of code. Written with sentences and paragraphs. Explain reasoning. Separated from subject by a blank line.  

**footer**: optional metadata or related information. ie: issue/bug tracker id, any breaking changes introduced.  


### Structure of Git

The "index" holds a snapshot of the content of the working tree, and it is this snapshot that is taken as the contents of the next commit. Thus after making any changes to the working tree, and before running the commit command, you must use the add command to add any new or modified files to the index.  

*work in progress*  
