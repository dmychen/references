# **EMACS Commands**  


## Getting Around Emacs

`C-x C-c` **->** Close emacs  
`C-x C-f` **->** open a file (or create new file)  
`C-x b`   **->** open a different buffer  
`C-x C-b` **->** open directory of current buffers  
`C-x d`   **->** open a directory (in dired mode)  

> When typing file path in minibuffer, press enter with no input to see the current directory  

`C-x o`   **->** focus on next window  
`C-x C-1` **->** close all windows but current one  
`C-x C-0` **->** close current window  
`C-x C-2` **->** split window to right  
`C-x C-3` **->** split window below  

> You can have multiple windows display the same buffer, if you want to edit different parts of one file.  


## Moving

`C-n` **->** next line  
`C-p` **->** previous line  
`C-f` **->** forward one character  
`C-b` **->** back one character  

`C-a`

Other commands include  

`M-{` **->** scroll up one paragraph  
`M-}` **->** scroll down one paragraph  
`C-v` **->** scroll down one page  
`M-v` **->** scroll up one page  
`M-<` **->** top of buffer  
`M->` **->** bottom of buffer  

`C-l`         **->** align cursor to middle of screen  
`M-g M-g NUM` **->** Go to line NUM  
`C-x C-=`     **->** text size++  
`C-x C--`     **->** text size--  

## Interacting with Text  

`C-k`     **->** Delete current line past cursor  
`M-DEL`   **->** delete word to left  
`M-d`     **->** delete word to right  
`C-x DEL` **->** delete sentence  

`C-SPC`   **->** Set mark  
`C-x C-x` **->** exchange mark with cursor  

> Set a mark then move cursor to select a portion of text!  
> Press C-g to deselect (but keep mark)  
> C-SPC C-SPC will set mark and push it onto the mark ring... press C-u C-SPC to restore  

`C-x TAB` **->** indent lines of text below cursor, up to paragraph end  
`M-^`    **->** append current line to previous line  

`C-s` **->** Searching for text. Press again to see next occurance. C-g to cancel. M-n/M-p for search history  

## When Lost  

`C-g` -> Cancel current command  
`C-h` -> Help!  

> After C-h, type one of the following:  
> b      **->** list keybindings  
> k KEYS **->** lists information about what the KEYS you just pressed do  
> m      **->** see current mode  

## Commands and Miscellaneous  

`M-!` **->** run a command as a one-off shell process  
`M-|` **->** take characters from selected region, pipes into shell command  

`M-x` **->** bunch of emacs commands  

> some basic ones:  
> shell -> opens shell in emacs  
> eshell -> idk similar thing  
> modename -> switch to another mode  


### More Emacs Resources  

[GNU](https://www.gnu.org/software/emacs/manual/html_node/emacs/ "GNU Emacs")  
[vinlin](https://github.com/vinlin24/cs35l-notebooks/blob/main/Emacs.md "VinLin Emacs Guide")  

