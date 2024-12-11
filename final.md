# Final AHHH

-   [Final AHHH](#final-ahhh){#toc-final-ahhh}
    -   [Version Control](#version-control){#toc-version-control}
        -   [History of Version
            Control](#history-of-version-control){#toc-history-of-version-control}
    -   [Git](#git){#toc-git}
    -   [Git\'s Internals](#gits-internals){#toc-gits-internals}
        -   [Structure](#structure){#toc-structure}
        -   [Internals](#internals){#toc-internals}
    -   [Git Commands](#git-commands){#toc-git-commands}
        -   [Local Changes](#local-changes){#toc-local-changes}
        -   [Displaying Info](#displaying-info){#toc-displaying-info}
        -   [Working with
            Remotes](#working-with-remotes){#toc-working-with-remotes}
        -   [Debugging Using
            Git](#debugging-using-git){#toc-debugging-using-git}
        -   [Config](#config){#toc-config}
        -   [Good Git
            Practices](#good-git-practices){#toc-good-git-practices}
    -   [C](#c){#toc-c}
        -   [Differences with
            C++](#differences-with-c){#toc-differences-with-c}
        -   [I/O](#io){#toc-io}
        -   [Strings](#strings){#toc-strings}
        -   [Memory
            Management](#memory-management){#toc-memory-management}
    -   [Defensive
        Programming](#defensive-programming){#toc-defensive-programming}
    -   [Compilation
        Process](#compilation-process){#toc-compilation-process}
        -   [User/Kernel Mode](#userkernel-mode){#toc-userkernel-mode}
        -   [Compilation](#compilation){#toc-compilation}
        -   [Compilation
            Process](#compilation-process-1){#toc-compilation-process-1}
    -   [GCC](#gcc){#toc-gcc}
    -   [Makefiles](#makefiles){#toc-makefiles}
    -   [GCC Options](#gcc-options){#toc-gcc-options}
        -   [Optimization Related
            Options](#optimization-related-options){#toc-optimization-related-options}
        -   [Debugging and
            Diagnostics](#debugging-and-diagnostics){#toc-debugging-and-diagnostics}
        -   [Code Generation
            Options](#code-generation-options){#toc-code-generation-options}
        -   [Language Feature
            Control](#language-feature-control){#toc-language-feature-control}
    -   [Debugging](#debugging){#toc-debugging}
	

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


### Debugging Using Git

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

### Config  

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
We use libraries for basic functions: `stdio.h` for `printf`.  


## C  

Core Language Philosophy:  

1) Procedural -> focused on functions and data separately, not object-oriented.  
2) Simplicity -> close to hardware, with fewer abstractions.  
3) Manual Memory Management -> no automatic cleanup mechanisms.  

### Differences with C++

- No classes or objects. Can't encapsulate data and methods. No inheritance or polymorphism.  
- No function overloading. Each function needs a unique name.  
- No references. Parameter passing always involves values or pointers.  
- No templates. Generic programming must use void pointers or macros. Type safety is managed manually.  
- No STL (no built-in containers... vectors, lists, maps).  
- No exception handling: error handling typically uses return values. Must check function returns explicitly.  
- No bool type for C89: use integers.  


`main` function: the entrance to our program, returns a value of type int.  

We use libraries for basic functions: `stdio.h` for `printf`.  

### I/O

`scanf("<specifier>", &var)` read input.  
`fgets(str, sizeof(str), stdin)` Safer input, with buffer limit.  
`read(int fd, void *buf, size_t count)` Read directly from a file, storing count bytes into buf. `fd = 0` is stdin.  
`write(int fd, const void *buf, size_t count)` Write count bytes from buf into a file fd. 
	
### Strings

`sizeof(str)` Total allocated memory for the string.  
`strlen(str)` Get length.  

`strcpy(dest, src)` Copy.  
`strncpy(dest, src, sizeof(dest) - 1)` Safely copy, supplying a max size.  

`strcat(dest, str)` Concatenate to end of dest.  
`strncat(dest, str, sizeof(dest) - strlen(dest) - 1)` Safely concatenate.  

`strcmp(str1, str2)` Compare two strings.  

`atoi("123")` String to int.  
`atof("3.14")` String to float.  
`strtol("123", NULL, 10)` String to long with base.  

	// Parsing strings
	char* token = strtok(str, " ,");
	while token != NULL) {
		printf("%s\n", token);
		token = strtok(NULL, " ,");
	}

**Format specifiers**

`%d` Integer  
`%.2f` Float with 2 decimals  
`%s` String  
`%c` Character  
`%p` Pointer  

    int num;
	char str[100];
	float fnum;

	scanf("%d", &num);     // Read integer
	scanf("%s", str);      // Read string (no & needed for arrays)
	scanf("%f", &fnum);    // Read float
	scanf("%[^\n]s", str); // Read entire line including spaces
	fgets(str, sizeof(str), stdin); // Safer string input

#### Structs
 
- Flexible array members must be last member.  
- pointer members require manual memory management.  

	// Structure with pointer members
	struct DynamicPerson {
		char* name; // Requires manual memory management
		int age;
		char** hobbies; // Array of strings
		int hobby_count;
	};
	
	// Function to initialize DynamicPerson
	struct DynamicPerson* createPerson(const char* name, int age) {
		struct DynamicPerson* person = malloc(sizeof(struct DynamicPerson));
		if (!person) return NULL;
		person->name = malloc(strlen(name) + 1);
		if (!person->name) {
			free(person);
			return NULL;
		}
		strcpy(person->name, name);
		person->age = age;
		person->hobbies = NULL;
		person->hobby_count = 0;
		return person;
	}
	
#### Function Pointers and Callbacks

Functions that are passed as an argument to other functions. A function pointer is a variable that stores the address of a function, allowing you to call the function indirectly through the pointer.  

	typedef int (*Operation)(int, int); 
	int apply(Operation op, int a, int b) {
		return op(a, b);
	}
	
	// Creates a type alias named Operation for a function pointer, taking two ints and returning an int.  
	// apply is a function that takes an Operation, a pointer to a function that takes two ints and returns an int.
	

#### Error Handling

In C, error handling is done through return values.  

	// Error/Exit codes
	enum ErrorCode {
		SUCCESS = 0,
		ERROR_MEMORY = -1,
		ERROR_INVALID_INPUT = -2,
		ERROR_FILE_NOT_FOUND = -3
	};
	
	// Function with error code
	int processData(const char* filename, int* result) {
		if (!filename || !result) return ERROR_INVALID_INPUT;
		// ... process data ...
		return SUCCESS;
	}
	
	// errno usage
	#include <errno.h>
	if (errno == ENOMEM) {
		// Handle out of memory
	}


### Memory Management

#### Memory Structure  

Memory is organized into regions that serve different purposes and have different *growth directions*. 

![memory-layout-c](https://images.javatpoint.com/cpages/images/memory-layout-in-c.png)


Memory is split into blocks.  
- each allocated blocks has metadata to track its size and status.  
- metadata stored in a header structure before the actual data.  
  - size_t size;  
  - int is_free;  
  - struct block_meta* next;  
  
Blocks are arranged as follows:  
- metadata block -> allocated memory -> next metadata block.  

Splitting blocks: if a free block is larger than request size, remainder can be kept as a smaller free block.  
- Coalescing adjacent free blocks: when multiple blocks are freed, allocator can merge them.  
- Fragmentation: heap becomes fragmented as many allocations/deallocations occur.  

Block selection: different algorithms can be used to choose which free block to allocate.  
- each one has different performance characteristics and fragmentation patterns.  
- First fit: searh for first block >= requested size. Quick but more fragmentation.  
- Best fit: Search for smallest block >= requested size. Slower but less fragmentation.  
- Worst fit: Search for largest block: good for splitting, poor memory utilization.  

 

#### Malloc Heap Management  

- If a free block exists in the heap that's large enough to satisfy the malloc request.  
- If no suitable block is available, the heap may be expanded by requesting memory from OS.  

	void* malloc(size_t size); // raw memory allocation  
	void* calloc(size_t num, size_t size) // Allocated zeroed  
	void* realloc(void* ptr, size_t size); // Resize allocation  
	void free(void* ptr); // Free memory  
	
	// Common allocation patterns
	
	int* intp = (int*)malloc(sizeof(int)); // cast void* to int*
	if (intp == NULL) return 1; // always check for success
	
	int* arrayp = (int*)malloc(n * sizeof(int));
	if (arrayp == NULL) return 1;
	
	struct Person* p = struct(Person*)malloc(sizeof(struct Person));
	if (p == NULL) return 1;
	
	int** matrix = (int**)malloc(rows * sizeof(int*));
	for (int i = 0; i < row; i++) {
		matrix[i] = (int*)malloc(cols * sizeof(int));
		if (matrix[i] == NULL) {
			// Handle error
			for (int j = 0; j < i; j++) {
				free(matrix[j]);
			}
			free(matrix);
			return 1;
		}
	}
		
	

#### System Call Interface  

- `malloc()` interacts with OS through system calls.  
- `sbrk()` and `brk()` are traditional UNIX system calls for managing program break.  
- modern systems use `mmap()` for large memory allocations.  

	void* sbrk(intptr_t increment); // increments size of program break by increment.  
	int brk(void* addr); // set program break to the specified location.  
	
	void* simple_malloc(size_t size) {
		static void* heap_end = NULL;
		if (heap_end == NULL) {
			heap_end = sbrk(0); // Get current break
		}
		void* block = sbrk(size);
		if (block == (void*)-1) {
			return NULL; // Out of memory
		}
		return block;
	}
	

## Defensive Programming

Anticipating and handling potential errors before they occur.  

Principles:  

1) **Never trust input** -> always validate outside data.  

2) **Boundary condition analysis** -> always check array bounds and buffer limits.  

3) **Error handling**  
- use assertions during development.  
- log errors and appropriate return values.  

4) **Memory safetly**  
- check that memory is allocated successfully before using it.  
- always free memory after use.  

5) **Contract programming**  
- check for pre and post conditions: the conditions incoming data must satisfy and form of output.  

6) **Logging and Tracing**  
- Log the level, file/line, time, and error string.  
- output to stderr and/or to a log file.  
- Trace entering and exiting a function, logging the start/end/duration time.

7) **Checkpoint and Recovery**  
- store checkpoints with a sequence number, a state of the application, and a timestamp.  
- create a checkpoint: write to stable storage a new checkpoint in sequence, containing the current state and metadata.  
- restore the latest valid checkpoint from stable storage.  

8) **Barricades**  
- implement security at trust boundaries:  
  - validate any data crossing the boundary.  
  - use type-safe interfaces.  
  - implement error handling.  
- validate by sanitizing strings, validating numeric ranges, defining allowed character sets, or in specific cases escaping SQL input, etc...  
- System-wide barricades:  
  - guard data packets with network data barricades.  
  - validate safe paths for files, checking for directory traversal (..), absolute paths, sanitizing allowed characters.  
  
9) **Safe Interpreter**  
- limit available operations.  
- implement resource quotas.  
- validate input before execution.  
- use strong typing.  

10) **Virtual Machines**  
- allow for safe execution:  
  - isolate execution environment.  
  - implement resource limits.  
  - system call filtering.  
  - monitor execution time.  
  - implement memory protection.  
- initialize with security constraints -> execute code in isolated environment (set up environment, start timer, check time limit and resource limits -> handle success and errors.  

## Compilation Process

### User/Kernel Mode

Desribes access to the system. Users are not given direct access to hardware. Kernel has complete access to hardware--can acccess any memory, issue any command.  

**System calls:** The way Users access kernel-level instructions.
- Ie: read, write, getpid, open, close are system calls.  
- Often system calls are used for I/O or disk operations...  
- Context switching (user <-> kernel) is expensive, we try to keep them to a minimum.  


> A user makes a sys call -> interrupt + swap to kernel -> kernel executes function -> flow returns to user mode with the output of the sys call.  

**Library calls** are higher level functions, the ones we interact with directly.  
- They function by making system calls, which are the only way to access kernel priviledges.  
- Ie: putchar, printf, etc...  

### Compilation

Turning a source file into a binary executable. We use a compiler such as gcc.  

`gcc -o prog prog.c` Compiles 

### Compilation Process

> Source Code -> Precompile -> Assembly -> Machine Code -> Executable Binary  

1. Preprocessing: Remove headers, macros, #define, comments from source code  

> #include <stdio.h>
> #define CONSTANT 5
> #ifdef ...
> // Some comment 

2. Compiler: Translate code to assembly language.  

3. Assembler: Assembly code to object file (machine code).  

4. Linker: Link imported libraries into code. This produces the final executable.  

**Static Linking**: directly copies library into the executable, at compile-time.  
- executable is self contained.  
- bulkier file, not flexible.  

**Dynamic Linking**: linked code is loaded at run-time.  
- requires `.dll` (dynamically linked library) or `.so` (shared object) files.  
- modular, but need to keep library files on the system.  


## GCC

Gnu Compiler Collection: Supports multiple languages, used widely for Unix/Linux.  

**`gcc -o OUTPUT SOURCES`**


- `-E` complete only preprocessing.  
- `-S` compile to assembly.  
- `-c` compile to an object file without linking.  

- `-I<DIR>` specify an include directory.  
- `-L<DIR>` specify the library linking path.  
- `-l<NAME>` link the library NAME.

Debugging:

- `-Wall` enable all common warnings.  
- `-Wextra` unused function paramters, missing field initializers, sign comparison issues.  
- `-Werror` Treat all warnings as errors.  

- `-O` optimize level. 0, 1, 2, 3.  
- `-Os` optimize for size over performance.  
- `-Og` optimize for debugging experience

- `-g` Enable debugging information you can  see in GDB: 1, 2, 3.

Other: 

- `-n` Dry run mode: print commands without running.  
- `-t` Update modification times of targets as if running commands without actually running it.  
- `-q` Check if targets are up to date without building.  
- `-f` specify a makefile name.  
- `-j` specify number of commands to run simultaneously.  
- `-C` change to specified directory before reading makefiles.  
- `-B` force rebuilding of all targets, even when up to date.  
- `-k` continue building other targets even when errors occur.  

## Makefiles

target: dependencies
	commands
	...
	
`*` wildcard.  
`%` match any string.  
`@` suppress comments.  
`-` add dash before a command to make it keep going even if the command fails.  
`$(VAR_NAME)` reference a variable.  
`foo = abc` to assign a value, or `foo := abc` to evaluate value at time of assignment.  

`$@` target name.  
`$<` first dependency.  
`$^` all dependencies.  
`$*` Stem

`.PHONY: RULES` Use phone to declare a phony target, one that has no output files.  


## GCC Options

### Optimization Related Options

#### Function Optimizations
■ -ffunction-sections # Place each function in its own section
■ -fdata-sections # Place each data item in its own section
■ -finline-functions # Integrate simple functions into their callers
■ -fno-inline # Don't integrate functions into their callers
■ -fomit-frame-pointer # Don't keep frame pointer in register
■ -foptimize-sibling-calls # Optimize sibling and tail recursive calls
#### Loop Optimizations
■ -funroll-loops # Unroll loops whose number of iterations can be
determined
■ -funroll-all-loops # Unroll all loops
■ -floop-optimize # Perform loop optimizations
■ -ftree-loop-vectorize # Vectorize loops
■ -floop-block # Block loops to improve cache performance
#### Code Size Optimizations
■ -ffunction-sections # Place each function in its own section
■ -fdata-sections # Place each data item in its own section
■ -fmerge-constants # Attempt to merge identical constants
■ -fmerge-all-constants # Attempt to merge all constants
■ -fno-common # Do not put uninitialized globals in common block

■ -march=native enable hardware intrinsics that perform better than their software counterparts. 

### Debugging and Diagnostics

#### Debug Information

■ -feliminate-unused-debug-types # Remove unused types from debug
info
■ -fno-eliminate-unused-debug-types # Keep all types in debug info
■ -fdebug-prefix-map=OLD=NEW # Remap debug info file paths
■ -fvar-tracking # Better debug info for optimized code

#### Runtime Checks, we talked

■ -fstack-protector # Enable stack protector
■ -fstack-protector-all # Enable stack protector for all functions
■ -fsanitize=address # Enable AddressSanitizer
■ -fsanitize=thread # Enable ThreadSanitizer
■ -fsanitize=undefined # Enable UndefinedBehaviorSanitizer

### Code Generation Options

#### Exception Handling

■ -fexceptions # Enable exception handling
■ -fnon-call-exceptions # Enable exceptions for non-call instructions
■ -fno-exceptions # Disable exception handling
■ -funwind-tables # Generate unwind tables for stack unwinding

#### Runtime Type Information

■ -frtti # Generate run-time type descriptor information
■ -fno-rtti # Disable run-time type descriptor information

#### Position Independent Code

■ a body of machine code that executes properly regardless of its
memory address.
■ -fpic # Generate position-independent code (small model)
■ -fPIC # Generate position-independent code (large model)
■ -fpie # Generate position-independent executable
■ -fPIE # Generate position-independent executable (large
model)

### Language Feature Control

#### C++ Features

■ -fno-enforce-eh-specs # Don't enforce exception specifications
■ -fstrong-eval-order # Enforce evaluation order of operands
■ -fno-threadsafe-statics # Don't generate thread-safe code for static
locals
■ -fvisibility-inlines-hidden # Hide inline function symbols

#### C Features

■ -fno-builtin # Not replace library functions with builtin compiled
code
■ -fno-asm # Don't recognize asm keyword

#### Compatibility Options

■ -fno-strict-overflow # Don't assume signed overflow wraps
■ -fwrapv # Assume signed arithmetic wraps
■ -fno-trapping-math # Assume FP operations don't trap

#### Common Option Combinations
 
Debug Build
■ CFLAGS="-fno-omit-frame-pointer -fstack-protector-all
-fsanitize=address -fvar-tracking -fno-inline"

Release Build
■ CFLAGS="-fomit-frame-pointer -ffunction-sections -fdata-sections
-fno-exceptions -fno-rtti -fvisibility=hidd


## Debugging

Debugging tools help us step through code, traceback calls, find values of parameters passed, manage memory.  

**Valgrind**: A tracing framework.  
- `gcc -g FILE.c -o FILE.exe` The -g flag tells gcc to include extra debugging information.
- `valgrind --leak-check=full ./file.exe` Show all information about memory leaks.  

**GDB**: Step through code line by line.  
- Check variable values, run commands, use breakpoints, traceback.  

`gdb a.out`
- `run [args]` or `run < file` Run the file with arguments.  
- `break [file]:LINE_NUM` Set breakpoint at line num, or by function name.  
- `info b` List breakpoints.  
- `delete/disable/enable NUM` Delete or disable a breakpoint by its breakpoint num.  
- `step [n]` Go to next n lines.  
- `next [n]` Go to next n lines, without going into functions.  
- `continue` Goes until next breakpoint.  
- `print var/exp` Print a variable or expression.  
- `watch var` or `rwatch var` Pauses when a variable is changed, or when a variable is read.  
- `list` List nearby lines.  
- `info` List info about a particular thing.  

- `attach pid` attach gdb to current running process, to debug something in production or running.  
- `backtrace` Show all the frames in the stack, one frame per line.  
- `watch` create a watchpoint: stops if object under watch changes.  
- `catch` create a catchpoint: stops for certain program events, (throws, exceptions, syscalls, etc...)  

- can debug a program on a target machine from a host machine: run program on target machine as `gdbserver :PORT_NUM ./buggy_program` and target it from host gdb with `target remote targethost:PORT_NUM`  


