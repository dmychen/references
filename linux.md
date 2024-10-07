# Linux Reference  

## Using Linux  

`man [command]` documentation for any command!  

> type '/' and words to search while in a manual.  
> press `n` next, `N` previous, `h` help, `q` quit  

### Basic Commands  

Directories

`pwd` print working directory.  

> . the current directory.  
> .. the parent directory.  
> ~ the home directory.  

`ls [directory]` list directory contents.  

> -l for long format.  
> -a for list all.  

`cd [directory]` change directory.  

`mkdir [directory]` make new directory.  

Files

`touch [file]` create a file.  

`rm [-r] [file]` remove a file. -r to delete a directory.  

`cp [src] [dest]` copy files. -r for directories.  

`mv [src] [dest]` move or rename a file.  

> Sidenote: there are a few characters that can be used in filenames to match certain characters.  
>   
> *: matches zero or any number of characters  
> ?: matches any one character  
> [...]: matches any one character in the list given in the bracket  
> {A,B}: matches either A or B  

File permissions are important!

`chmod [options] mode[,mode] file1[file2...]` change user permissions to a file.

> How permissions work  
>   
> Shown as 10 bits, 1st bit represents a directory, then three groups of three representing permissions for different groups.  
>   
> owner (u)  
> group that owns the file (g)  
> others (o).  
>   
> \+ to add permissions, \- to remove, = to set permissions.  
>   
> ie: drw-rw-x--- -> chmod u+x filename -> drwxrw-

Here are a few commands relating to file contents. All these commands output their results, they don't manipulate the original input file.  

`grep [options] PATTERN [files]` searches for PATTERN in a file or files. There are several options to change the behavior of grep.   

> `-c` returns instead a count of lines that match a pattern  
> `-h` display the matching lines, without filename  
> `-i` ignore case for matching  
> `-n` display line numbers  

`sort [options] FILE` sorts a file alphabetically by line. Number before uppercase before lowercase.  

> -o specifies output file (equivalent to redirecting).  
> -r reverse order.  
> -n sorts numerically.  
> -c checks if file is sorted. Returns any disorder.  
> -u removes duplicate items.  

`tr [options] SET1 SET2` "translate". Supports several transportations, from deleting to find and replace. SET1 and SET2 are sets of chars.   

> `-c` applies operation to characters not in the given set.  
> `-d` deletes characters in first set.  
> `-s` replace repeated characters in SET1 with single occurance of that char.  

`comm [options] FILE1 FILE2` compares two lexically sorted files line by line. Generates 3 column output: lines unique to FILE1, unique to FILE2, common to both files.  

> `-1` suppress column 1 (don't display lines unique to FILE1).  
> The same applies to -2 and -3.  
> `-i` ignores case.  
> `-check-order` check if input is sorted.  
> `-nocheck-order` ignores if files are sorted.  


### Creating Bash Scripts  

Can write and execute bash commands in a bash script, not just in the command line. Bash scripts have the form `NAME.sh`. The script can be run with `bash NAME.sh`.  

Can **create a variable** `NAME=[value]`, and access the value of that variable, `$(NAME)`. The output of a command can be stored in a variable `var=$([cmd])`.  


**Standard input** can be read into variable NAME with `read NAME`.   

**Input from a file** can be read and written as follows:  

`[cmd] < file` input from a file.  
`[cmd] > file` or `[cmd] 1> file` standard output to a file.  
`[cmd] 2> file` standard error to a file.  
`[cmd] >> file` append to a file (no overwrite).  


**Piping** the stdout of [cmd1] as the stdin of [cmd2] can be done with `[cmd1] | [cmd2]`.  


> More bash resources:  
> [scripting-tutorial](https://www.shellscript.sh/ "The shell scripting tutorial!")  
> [learn-bash-in-minutes](https://learnxinyminutes.com/docs/bash/ "learn x in y minutes where x=bash")  
> [shell-command-language](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html "Shell command language guide")  

## Understanding Linux  

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
