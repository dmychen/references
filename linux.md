# Linux Reference  

## Linux Commands  

General commands:

`man [command]` Documentation for any command.  

> type '/' to search while in a manual.  
> press **n** next, **N** previous, **h** help, **q** quit to navigate.  


`echo [options] [string]` Prints the string in command line.  

> `-e` allows for **\n** as newline.  

`which [program]` locate the program file for a command. 

### Directories  

`pwd` Print working directory.  

> . the current directory.  
> .. the parent directory.  
> ~ the home directory.  


`ls [directory]` List directory contents.  

> `-l` for long format.  
> `-a` to list all.  
> `-R` for recursive.  
> `-t` to show time and order by time.  
> `-d` to only show directories.  
> `-i` to show each file's unique identifier.  



`cd [directory]` Change directory.  

`mkdir [directory]` Make new directory.  


### Files  

`touch FILE` Create a file.  

`rm [opt] FILE` Remove a file.  

> `-r` to delete a directory.  
> Not safe removal, can't recover.  
> Don't do: `rm -rf ~/`

`cp SRC DEST` Copy files. `-r` for directories.  

`mv SRC DEST` Move or rename a file.  

`cat FILE`

> Sidenote: there are a few characters that can be used in filenames to match certain characters.  
>   
> *: matches zero or any number of characters  
> ?: matches any one character  
> [...]: matches any one character in the list given in the bracket  
> {A,B}: matches either A or B  


File permissions are important.

`chmod [options] mode[,mode] file1[file2...]` Change user permissions to a file.

> How permissions work:  
>   
> 10 bits:
> 1st bit -> **-** for file, **d** for directory, **l** for symbolic links.
> 3 groups of 3 bits -> **r** read permission, **w** write permission, **x** execute permission, **-** permission denied.  
>   
> The three groups represent, in order:  
>   
> owner (u)  
> group that owns the file (g)  
> others (o).  
>   
> \+ to add permissions, \- to remove, = to set permissions.  
>   
> ie: `-rwxrw-r-- filename` -> normal file, user has read/write/execute permissions, group has read/write permissions, others has read permissions.  
> `chmod g+x filename` -> now the permissions look like this: -rwxrwxr--  



### Manipulating Files  

Here are a few commands relating to file contents. All these commands output their results, they don't manipulate the original input file.  

`grep [options] PATTERN [files]` Searches for PATTERN in a file or files. There are several options to change the behavior of grep.   

> `-c` returns instead a count of lines that match a pattern  
> `-h` display the matching lines, without filename  
> `-i` ignore case for matching  
> `-n` display line numbers  
>   
> More information on regular expressions in regex.md.  

`sed s/old/new/g] filename` Replace patterns matching **old** with **new** in **filename**.


`sort [options] FILE` Sorts a file alphabetically by line. Number before uppercase before lowercase.  

> -o specifies output file (equivalent to redirecting).  
> -r reverse order.  
> -n sorts numerically.  
> -c checks if file is sorted. Returns any disorder.  
> -u removes duplicate items.  


`tr [options] SET1 SET2` "Translate". Supports several transportations, from deleting to find and replace. SET1 and SET2 are sets of chars.   

> `-c` applies operation to characters not in the given set.  
> `-d` deletes characters in first set.  
> `-s` replace repeated characters in SET1 with single occurance of that char.  


`comm [options] FILE1 FILE2` Compares two lexically sorted files line by line. Generates 3 column output: lines unique to FILE1, unique to FILE2, common to both files.  

> **-1** suppress column 1 (don't display lines unique to FILE1).  
> The same applies to -2 and -3.  
> `-i` ignores case.  
> `-check-order` check if input is sorted.  
> `-nocheck-order` ignores if files are sorted.  


`ln [source] [target]` Creates a new directory entry (linked file) for the file **source**.

> **target** file has the same file modes as **source** file. A link points to the original copy, either via a hard link or a symbolic link.  
> By default, `ln` makes hard links. Hard links are the indistinguishable from the original file.  
> `-s` creates a symbolic link. Symbolic links contain the name of the file that it points to. 


### Processes

`ps -u` Displays processes owned by the specified user.
`ps -e` Shows all processes on the system.
`ps aux` Common combination of options that provides a comprehensive process listing.



## Bash Scripts  

We can write and execute bash commands in a **bash script**, not just in the command line. Bash scripts have the form **NAME.sh**. The script can be run with `bash NAME.sh`.  

### Writing a Bash Script  

    #!/bin/sh  
	# This is a comment  
	echo Hello World  

Starting with` #!/bin/sh` tells Unix to execute a file **file.sh** via **/bin/sh**.  
Comments are written with **#** in Bash scripting.  
	
> The **#** on the first line is treated specially, not as a comment. It tells Unix that disregarding what shell you're using (csh, ksh, etc), the file should be interpreted by the Bourne shell. Other scripts work similarly, ie `#!/usr/bin/perl` for a Perl script.  


Another note: the shell parses arguments before passing them to the program being called. For example in `echo *`, ***** is expanded to reference all files in the current directory before being passed to echo.  


### Variables  

`VAR=value` Assign a variable with value.  

> We can also assign the output of a command to a variable, `VAR=[cmd]`.  
> Remember not to put spaces around the **=**.  


`$VAR` Accesses the value stored in **VAR**.  
`read VAR` Reads a line from stdin into **VAR**.  


There is no type checking in bash scripts, everything is stored as a string.  

Reading an undeclared variable results in an empty string, with *no warnings or errors*.  

We can enclose a variable in curly braces `${VAR}`. This makes it clear where the variable name ends.

> For example `touch "${USER_NAME}_file"` works, while `touch "$USER_NAME_file"` would not, given a variable **$USER_NAME**.  

Accessing arguments for a script:

`$[num]` Accesses arg[num].

> `${2}` accesses arg2, `${10}` accesses arg10

`$@` Represents all arguments passed to a script or function.

Another note. 

`$$` Current processor ID


### Redirection   

Input and output from files can be **redirected** as follows:  

`[cmd] < file` input from a file.  
`[cmd] > file` or `[cmd] 1> file` standard output to a file.  
`[cmd] 2> file` standard error to a file.  
`[cmd] >> file` append to a file (no overwrite).  
`[cmd1] | [cmd2]` "pipes" the stdout of [cmd1] as the stdin of [cmd2].   


### Scoping  

When a **file.sh** is ran from our interactive shell, a new shell is created to run the script.  

> Our script **file.sh** will not inherit values from variables in our interactive shell.  

`export VAR` Allows another program, such as our script, to inherit that variable.  

`. ./file.sh` Sources the script, which basically runs **file.sh** within our own shell.  


### Loops  

idk

-------------------------------------------------------------------------------

More bash resources here:  

> [scripting-tutorial](https://www.shellscript.sh/ "The shell scripting tutorial!")  
> [learn-bash-in-minutes](https://learnxinyminutes.com/docs/bash/ "learn x in y minutes where x=bash")  
> [shell-command-language](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html "Shell command language guide")  



## Understanding Linux's Structure  

### The Shell  

The shell is itself a program, a file executed by the operating system.

**sh** is the predecessor to **bash** 



Linux is a family of "open-source unix-like operating systems" based on linux kernel.  

The **shell** is a command-line interpreter (CLI) that provides a command line user interface. Typically use a terminal to access the unix shell.  

> The shell takes user commands and passes them to OS to execute.  


Unix files are organized in a **tree structure**, making even a lot of data easy to manage. The unix file system contains directories and files (at least at a basic level).  

Here are some of the most important directories  

> `/` root directory. The highest level.  
> `home` contains user directories and files  
> `root` the root users' home directory (note this is different than /)  
> `bin` the directory where many commonly used executable commands reside (short for binaries).  
> `usr` also contains executable commands  

And some more directories:  

> `dev` contains device specific files  
> `etc` contains system configuration files  
> `lib` contains all library files  
> `mnt` contains device files related to mounted devices  
> `proc` contains files related to system processes  
> `sbin` system binary files reside here. If there is no sbin directory on your system, these files most likely reside in etc  
> `tmp` storage for temporary files which are periodically removed from the filesystem  
