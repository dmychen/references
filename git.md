# **Git and Github**  

## Git Commands  

`git init` creates new repo tracking current directory.  

`git clone` creates local copy of remote project. Includes files, history, backups.  

`git add` stages current change. (Added to index).  

`git status` status of changes: untracked, modified, staged.  

`git commit` saves staged changes to the project's history.  

> `git commit -m "MESSAGE-HERE"` to add a commit message from command line.

`git branch` shows branches being worked on locally.  

`git merge` merge branches.  

`git pull` updates local repo with updates from remote repo.  

`git push DEST SRC` updates remote repo with commits made to local branch.  

`git remote -v` shows information about the remote repo


Comprehensive list of commands can be found at [gitDocs](https://git-scm.com/docs "git commands documentation").  


## About Git

### What does Git do

Git Controls 3 things:  
1. working files (source code, current state of repository)  
2. history of project development. modeled with a tree of files  
3. index. "recording plans for the future".  


### Setting Up a Repository  

Clone a remote repository onto local environment  

> `git clone REMOTE-URL`  

OR: Create a local repository, and link it to a remote repository. Make sure the remote repository is empty.

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
