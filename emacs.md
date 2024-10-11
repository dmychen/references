# **EMACS**  

## Controls in EMACS  

To get out of a pickle...

`C-x C-c`  Close emacs.  
`C-g` Cancel current command.  
`C-h` Help!  

>  After C-h, you can type one of the following:  
> `b`       list keybindings  
> `k KEYS`  lists information about what the KEYS you just pressed do  
> `m`       see current mode  

Another note: whenever Emacs automatically opens a buffer for you, you can close that buffer by focusing on it with `C-x o` and pressing **q** to close it.

### Files and Buffers  

Everything in Emacs is loaded in a **buffer**, which disappears when Emacs is closed. Files are all opened, edited, and saved within an Emacs buffer.  

> The **minibuffer** is a special buffer that opens whenever we read in complicated arguments, such as file and buffer names, emacs commands, or lisp expressions. The **Messages** buffer that emacs provides shows a running history of the minibuffer's output.  


`C-x C-f`  **Open a file**, or create new file if it doesn't exist.  

> You can press enter without typing a file name to see the current directory.  


`C-x d`    **Open a directory**  (in *dired mode*)  
`C-x C-b`  Open a directory of the current buffers in emacs.  

> When viewing a directory, press **d** to mark a file for deletion, press **x** to confirm deletion.  


`C-x b`    **open a buffer** (default last buffer)  
`C-x k`    close a buffer (default current buffer)  

> `C-x b RET` will open the previous buffer, which is very useful when you are using multiple buffers with one window. `C-x k RET` will similarly close the current buffer.  


### Frames (Windows)  

Emacs calls different windows "frames". Each frame contains a buffer, and multiple frames can contain the same buffer. This can be useful if you want to access different parts of a long file at the same time.  

`C-x o`    change focus to the next frame.  
`C-x C-1`  close all frames but the current one.  
`C-x C-0`  close current frame.  
`C-x C-2`  split frame to right.  
`C-x C-3`  split frame below.  

> **q** will close a frame that Emacs automatically opened for you, if you are focused on that buffer. Useful for example when you open a directory with `C-x C-f RET` or look up a command with `C-h m`.  


### Moving Around A Buffer

`C-n`  next line  
`C-p`  previous line  
`C-f`  forward one character  
`C-b`  back one character  

These two are the ones I use most:

`C-a`  beginning of the line  
`C-e`  end of the line  

For even more efficient movements, use:

`C-M-f` forward over balanced expression  
`C-M-b` backwards over balanced expression  
`C-M-n` forward to next parenthetical group  
`C-M-p` backwards over previous parenthetical group  

For big movement, we have these:  

`M-{`  scroll up one paragraph  
`M-}`  scroll down one paragraph  
`C-v`  scroll down one page  
`M-v`  scroll up one page  
`M-<`  top of buffer  
`M->`  bottom of buffer  

Some other commands:  

`C-l`          align screen so cursor is in the middle of whats shown in the buffer.  
`M-g M-g NUM`  Go to line NUM  
`C-x C-=`      text size++  
`C-x C--`      text size--  


### Interacting with Text  

**Deletion**:  

`C-k`      delete current line, past cursor  
`M-DEL`    delete word to left  
`M-d`      delete word to right  
`C-x DEL`  delete sentence to left  

**Spacing**:  
  
`C-x TAB`  indent lines of text within the region (see "mark" for more info).  
`M-^`      append current line to previous line.  

**Searching**:  

> Emacs searches for occurrences of a string starting at where the pointer is. Pressing the search button again will move to the next match. Once it hits the end of the buffer, it will start the search from the top.

`C-s`  **Search** for a text string.  
`C-r`  Search in reverse.  
`C-M-s` Search by *regexp*.  

> Press `C-s` again to see next occurrence. Press `RET` to place cursor at the current search result. `C-g` to cancel search.   

`M-%` **Find and replace**. 
`C-M-%` Find and replace a *regexp*. Same applies.  
`M-x replace-string` Replaces all instances of a string in one go.  

> For each occurrence, press  
> `y` or `SPC` to replace.  
> `n` or `DEL` to skip.  
> `^` to go to previous occurrence.  
> `u` to undo the last replacement, and go back to that point.  
> `U` to undo all replacements, and go back to the start.  
> `!` to replace remaining occurrences.  


**Marks**:  

Emacs has something called a **mark**, which is a saved location in the buffer. Everything between this saved mark and your cursor is called the **region**, which basically means a selected chunk of text.  

The mark allows for more advanced movement and manipulation of text. You can jump to the position of the mark at any time, and you can execute commands on the region between the mark and your cursor.

> For example: to copy a region of text, you can place a mark at the beginning of what you want to select, move your cursor to the end of what you want to select, and press the copy key. This will copy everything from the mark to your cursor.  

`C-SPC`    Set mark. This sets a mark at your current location.  

> If you move your cursor immediately after setting a mark, the region between the mark and your cursor will be highlighted. If you do a non-movement operation, the region will no longer be highlighted, but doesn't disappear. You can also press `C-g` to unhighlight.  

`C-x C-x`  exchange mark with cursor.  

> This allows you to jump wherever your mark is. Useful if there's a place in the file you want to repeatedly go back to.

`C-SPC C-SPC` Set's mark and push it onto the mark ring.

> Kinda confusing, but this creates a mark and then deactivates it. The mark ring is basically a history of your previous marks, which you can still access.

`C-u C-SPC` Restore "pop" mark off of the mark ring.  

> Allows you to use previous marks. idk.

The mark is really useful for copying and cutting text. It's also great if you need to indent multiple lines. You can use `C-x TAB` to indent everything in the region. 

## Commands, Shell, and Customization  

### Commands
 
The **commands** we use in Emacs, including all keyboard shortcuts above, are each tied to a identifying name. Not all commands necessarily have a keyboard shortcut. All commands in Emacs can be run by calling their name.  

`M-x [command]` Calls a command by its name.  

You can search for some of the commmands emacs has with `C-h a` or see documentation for a specific command with `C-h x`


Emacs also has internal **variables**, which we sometimes manipulate when changing settings or customize Emacs.  

`M-x describe-variable` Accesses a variable's function and value.  

> Also accessed through `C-h v`.  

Emacs can run a **shell**, without needing to go to terminal.  

`M-x shell` Opens shell in emacs.  
`M-x eshell` idk very similar.  

> `M-!`  Run a single shell process in the minibuffer.  
> `M-|`  Take characters from selected region, and pipe it into a shell command.  


### Modes in Emacs  

Emacs has different *major* and *minor* **modes**. These modes change the behavior of Emacs, and are set per buffer. Emacs automatically picks a mode based on what the buffer is doing (when editing a latex file, emacs goes into latex mode, when editing a lisp file, enters lisp mode).

`C-h m` Show information on the current major mode. Includes keybindings and other information.  
`M-x modename` switch to another qzzxyamode.  

`M-x electric-pair-mode` Toggles [electric-pair-mode](https://www.emacswiki.org/emacs/ElectricPair), which inserts matching delimiters.  


### Emacs Lisp  

Emacs runs on Lisp. To customize the behavior of Emacs, we often put Lisp code in an `.emacs` file, which runs when Emacs is initialized. Reload the `.emacs` file after editing it with `M-x load-file`. more information at [init-file-manual](https://www.gnu.org/software/emacs/manual/html_node/efaq/Setting-up-a-customization-file.html).  

To evaluate some Lisp code while in Emacs, write it out in the *scratch* buffer that emacs provides, and press `C-j` to evaluate.  

Y->ou can also execute Lisp in any normal buffer by typing `C-x C-e`, which will evaluate code immediately behind the pointer.  

Typing `M-x eval-expression` lets you write Lisp in the minibuffer. Prepend `C-u` to insert output in buffer, instead of displaying it in minibuffer.  


Emacs has a bunch of packages that allow us to customize all sorts of things.  

`M-x list-packages` See available packages you can install for emacs.  

> When looking for packages, use `i` to mark a package for installation, and `x` to install.  


## Backups and Autosaving  

Emacs automatically makes backups and auto-save files. Auto-saving preserves the text from earlier in the current editing session. Backup files preserve the contents of the file you're editing from before your current editing session.  

Auto-save files have the form `#foo#`, and I think they go away after your current editing session. Backup files have the form `foo.~num~` where num is the number of the backup.  

These files are automatically put in your working directory, which can become a bit messy. To change this, you can redirect backup files elsewhere.  

> You can make all backup files go into a directory by putting something like the following in your .emacs.  
>   
>    `(setq backup-directory-alist `(("." . "~/.saves")))`  
>   
> There are a number of arcane details associated with how Emacs might create your backup files. Should it rename the original and write out the edited buffer? What if the original is linked? In general, the safest but slowest bet is to always make backups by copying.  
>   
>    `(setq backup-by-copying t)`  
>   
> Since your backups are all in their own place now, you might want more of them, rather than less of them. Have a look at the Emacs documentation for these variables (with C-h v).  
>   
>     (setq-old-versions t  
>     kept-new-versions 6  
>     kept-old-versions 2  
>     version-control t)  
>   
> Finally, if you absolutely must have no backup files:  
>   
>     (setq make-backup-files nil)  

This is pulled from [this post](https://stackoverflow.com/questions/151945/how-do-i-control-how-emacs-makes-backup-files).  

More Information about Backups and Auto-Saving: [backups-a
utosaving](https://www.math.utah.edu/docs/info/elisp_24.html#SEC341 "Backups and Auto-Saving").  


-------------------------------------------------------------------------------  

### More Emacs Resources  

[GNU](https://www.gnu.org/software/emacs/manual/html_node/emacs/ "GNU Emacs")  
[vinlin](https://github.com/vinlin24/cs35l-notebooks/blob/main/Emacs.md "VinLin Emacs Guide")  

