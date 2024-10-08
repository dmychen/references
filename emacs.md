# **EMACS**  

## Emacs Controls  

The most basic commands  

`C-x C-c`  Close emacs  
`C-g` -> Cancel current command  
`C-h` -> Help! If it opens a new buffer, you can close it by pressing `q` while focused on it.  

> After C-h, you can type one of the following:  
> `b`       list keybindings  
> `k KEYS`  lists information about what the KEYS you just pressed do  
> `m`       see current mode  


### Files and Buffers  

Everything in Emacs is loaded in buffers, which disappear when Emacs is closed. A file can be opened, edited, and saved within an Emacs buffer.  

> The minibuffer is a special buffer that opens whenever we read in complicated arguments, such as file and buffer names, emacs commands, or lisp expressions. The **Messages** buffer that emacs provides shows a running history of the minibuffer's output.  


`C-x C-f`  open a file, or create new file if it doesn't exist.  

> You can press enter without typing a file name to see the current directory.  


`C-x d`    open a directory (in dired mode)  

> When viewing a directory, press `d` to mark a file for deletion, press `x` to confirm deletion.  


`C-x b`    open a buffer (default last buffer)  
`C-x k`    close a buffer (default current buffer)  

> `C-x b RET` will open the previous buffer, which is very useful when you are using multiple buffers with one window. `C-x k RET` will similarly close the current buffer.  


`C-x C-b`  open directory of current buffers  


### Emacs Windows  

`C-x o`    focus on next window  
`C-x C-1`  close all windows but current one  
`C-x C-0`  close current window  
`C-x C-2`  split window to right  
`C-x C-3`  split window below  

> You can have multiple windows display the same buffer, if you want to edit different parts of one file.  


### Moving Around

`C-n`  next line  
`C-p`  previous line  
`C-f`  forward one character  
`C-b`  back one character  

`C-a`  beginning of the line  
`C-e`  end of the line  

`C-M-f` forward over balanced expression  
`C-M-b` backwards over balanced expression  
`C-M-n` forward to next parenthetical group  
`C-M-p` backwards over previous parenthetical group  

For bigger movement, you can use:  

`M-{`  scroll up one paragraph  
`M-}`  scroll down one paragraph  
`C-v`  scroll down one page  
`M-v`  scroll up one page  
`M-<`  top of buffer  
`M->`  bottom of buffer  

And some other movement commands.  

`C-l`          align cursor to middle of screen  
`M-g M-g NUM`  Go to line NUM  
`C-x C-=`      text size++  
`C-x C--`      text size--  


### Interacting with Text  

`C-k`      delete current line past cursor  
`M-DEL`    delete word to left  
`M-d`      delete word to right  
`C-k`      delete line to right  
`C-x DEL`  delete sentence to left  

`C-SPC`    Set mark  
`C-x C-x`  exchange mark with cursor  

> Set a mark then move cursor to select a portion of text!  
> Press C-g to deselect (but keep mark)  
> C-SPC C-SPC will set mark and push it onto the mark ring... press C-u C-SPC to restore  


`C-x TAB`  indent lines of text below cursor, up to paragraph end  
`M-^`     append current line to previous line  

`C-s`  Searching for text. Press again to see next occurance. C-g to cancel. M-n/M-p for search history  



## Commands, Lisp, Shell  

### Commands

All commands in emacs are tied to a name. Many common commands are also tied to a keyboard shortcut, like the ones above. However, all commands in emacs can be run by calling their name.  

`M-x [command]` Calls a command by its name. Here are some common commands.  

`M-x describe-variable` Access a variables function and value.

> Also accessed through `C-h v`.


`M-x shell` opens shell in emacs.  
`M-x eshell` idk very similar.  

> `M-!`  To run a one-off shell process in the minibuffer.  
> `M-|`  To take characters from selected region, and pipe it into a shell command  


`M-x list-packages` See available packages you can install for emacs.  
`M-x eval-expression` Write Lisp code.  

> When looking for packages, use `i` to mark a package for installation, and `x` to install.  


`M-x modename` switch to another mode.  

> `C-h m` will show information on the current major mode.  




### Emacs Lisp

Emacs runs on Lisp. To customize the behavior of Emacs, we often put Lisp code in an `.emacs` file, which runs when Emacs is initialized. Reload the `.emacs` file after editing it with `M-x load-file`. Find more information at [init-file-manual](https://www.gnu.org/software/emacs/manual/html_node/efaq/Setting-up-a-customization-file.html).  

To evaluate some Lisp code while in Emacs, write it out in the *scratch* buffer that emacs provides, and press `C-j` to evaluate.  

You can also execute Lisp in any normal buffer by typing `C-x C-e`, which will evaluate code immediately behind the pointer.  

Typing `M-x eval-expression` lets you write Lisp in the minibuffer. Prepend `C-u` to insert output in buffer, instead of displaying it in minibuffer.  


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
>     (setq delete-old-versions t  
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

