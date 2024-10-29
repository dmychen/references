# Markdown Reference  

## Shortcuts In Emacs  

For a list of all keyboard commands, press  

> C-c C-h

To manipulate the current markdown file:  

> C-c C-c CHAR  

Here are the important commands  

> `m`: show output html in buffer  
> `p`: create temporary preview file in browser  
> `e`: export basename.html  
> `v`: export basename.html and open in browser  
> `l`: opens live preview in \*eww\* buffer  

For text formatting you can use  

> C-c C-s CHAR  



### Text Formatting  

Headings are symbolized as followed. Remember to put a space before your text.  

> Heading 1: # *text here*  
> Heading 2: ## *text here*  
> Heading 3: ### *text here*  

You can bold or italics with *. 
If you want to use the * character without bolding/italicizing, backslash before the *. 

> **bold**: \*\**text goes here\*\**  
> *italics*: \**text goes here\**  


### Not native to Markdown  

Center text  

> `<p style="text-align:center">Center this text</p>`  

Indent by one space  

> `&nbsp;`  

Underline

> `Some of these words <ins>will be underlined</ins>.`
