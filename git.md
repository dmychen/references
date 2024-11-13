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

## Git 

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

 Object files are the core storage of git's data. Indexed via a 40-character SHA-1 hash.  


**Trees**: represent directory structure of your projectat a specific point of time. Link blobs together. Like a folder.  
- contains hashes of sub-trees and blobs, along with the parent.  

**Blobs**: represents content of individual files. Each version of a file stored as a blob.  
- doesn't store metadata, just the content. Name corresponds to their SHA-1 hash.  

- Chunks of data with associated ID/hash
- `git show HASH` Show blob corresponding to hash.  
- `git hash-object FILE` Shows hash corresponding to file.

**Commits/Snapshots**: represents snapshot of project's history. Contains a pointer of a tree, info about author and commit message. Pointers to parent commits. (Forms commit history graph, the DAG).  
- Git saves space by using pointers -> if nothing changes don't have to store anything new.  
- Each object has a unique Hash 

Checksums: SHA-1 Hashing -> hexadecimal hash based on contents of a file.  

Git sometimes packs several objects into a single binary (packfile)
- Automatically happens when: loose objects, pushing to remote surver, running `git gc`

### Internals  

**HEAD:** Points to current index: current commit and branch.  

**config:** File that contains config information.  

**refs/:** A folder that contains: heads, remotes, tags.  
- heads: Folder that contains, for every branch, where the head is. Stored as SHA-1 hashes.  
- remotes: Folder containing remote repositories.  
- tags: tags are tied to a commit.  

**hooks/:** For automation. Can create scripts that run whenever a commit, merge, patch, etc... occurs.  

**objects/:** Where the bulk of stuff is stored! Holds all object files.  
- includes: commits, trees, files (blobs).  
- Stored in folders corresponding to the first 2 digits of a given object's hash.  
- Use `git cat-file -p HASH` to see the internals of an object file.  


## Using Git  

`git help <command>` Get help on a Git command.  

### Changing Local  

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
- 

**`git restore`** 
- `--staged` 

**`git tag "PATTERN"`** Tag points in repo history (ie. release points, etc.). Pattern is optional.  
- `-l` optional list flag.  
- `-a` annotated tags: stored as full objects. 
- `-m` Specify tagging message, stored with tag.  
- lightweight tags: Automatic if no specifying option. 'unchanging branch', points to specific commit.  
- `-d NAME` Delete a tag

**`git format-patch COMMIT`** Create patch files

### Display Info  

**`git cat-file HASH` Show information about an object file.  
- `-p` Pretty print. Prints...  
  - The tree's hash: the 
  - The parent's hash: the parent of the current node (current commit).  
- `-t` Shows type of the object file. (commit, tree, file)  


**`git status`** Status of changes: untracked, modified, staged.  
- `-s` or `--short` Simplified output.  

**`git branch`** shows branches being worked on locally.  
- `-D` Delete a branch.  
- `-M` Rename a branch.  

**`git diff COMMIT..COMMIT`** Shows added and removed lines. By default only shows changes that are unstaged.  
- `--staged` or `--cached` See staged changes. Compares to last commit.  
- no arguments -> see changes since last commit (see unstaged changes).  

**`git log`** Lists commits made in repository in reverse chronological order.  
- `-p` or `--patch` shows difference introduced in each commit.  
- `-<n>` Only show n number of previous entries.  
- `--stat` See abbreviated stats for each commit.  
- `--pretty=TYPE` Change log format: oneline, short, full, fuller, format (manually decide log format).  
- `--graph` Ascii graph showing branch and merge history.  
- `--since` for commits after specified date, or `--until` for commits before specified date.  

`git cat-file -p HASH` Use on a commit hash. idk what it does.  

**`git reflog`** Log of all git changes that have happened in the repository. Useful if you ever do anything crazy or anything goes wrong.  
- can reset to a previous state (`git reset --hard HASH`).  

### Work with Remote  

**`git clone URL`** Creates local copy of remote project. Includes files, history, backups.  
- Creates a directory and initializes it.  

**`git remote`** Displays remote servers.  
- `-v` Shows more information about the remote servers.  
- `add SHORTNAME URL` Add a new remote repository.  
- `show REMOTE` Lists information about the remote server.  
- `rename OLD NEW` Rename a remote's shortname.  

**`git fetch REMOTE`** Pulls all changes from remote repo to local, without merging it with local repo.  

**`git merge`** merge branches.  
- `--squash` Creates a single commit for idk?  
- `--continue` Continue merge after resolving merge conflicts.  


**`git rebase`** 

**`git pull`** Automatically fetch from remote and merge with current branch.  

**`git push REMOTE BRANCH`** Push branch to remote server. Only works if you are up to date with updates to remote.  
- can push a tagname as well, or use `--tags` option to transfer all tags.  


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
