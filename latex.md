# LaTeX  


## Writing Latex with AUCTex  

`C-c TAB` Read AUCTex Manual!

> For most commands, press `TAB` or `SPC` to see available options.  


### Spacing


`C-c C-s` Insert section.  
`C-c C-e` Insert environment.  
`C-c RET` Insert macro.  



### Math Mode  

`C-c ~` Toggles math mode. 

> Add `(add-hook 'LaTeX-mode-hook #'LaTeX-math-mode)` to init file to enable Math mode by default.  

When in math mode, prepend ``` to keywords to write math symbols.

> Can customize `LaTeX-math-list` to change things.


### Previewing and Compiling Latex  

`C-c C-p C-p` Preview at pointer.  
`C-c C-p C-e` Preview environment.  
`C-c C-p C-r` Preview region.  
`C-c C-p C-b` Preview buffer.  
`C-c C-p C-d` Preview document.  

To remove previews, use `C-c C-p C-c [type]` where [type] are the above options.  


`C-c C-a` Compiles the Latex document.  

> Runs LaTeX until document is ready, and opens output document in viewer.  

`C-c C-c` Does individual compilation activities by default.  

> Decides which action to do based on context. Can pick what action you want as well, such as `Clean` and `Clean All` to delete auxiliary files.  

`C-c C-t C-p` Toggles compilation between PDF and DVI mode.  

`C-c C-t C-i` Stops on errors (Interactive mode).  

`C-c C-v` View output file.  

[Debugging-info](https://www.gnu.org/software/auctex/manual/auctex/auctex_25.html#Debugging-LaTeX) can be found here.  


### Fontsetting

`C-c C-f C-b` Insert bold face ‘\textbf{∗}’ text.  
`C-c C-f C-i` Insert italics ‘\textit{∗}’ text.  
`C-c C-f C-e` Insert emphasized ‘\emph{∗}’ text.  
`C-c C-f C-s` Insert slanted ‘\textsl{∗}’ text.  
`C-c C-f C-r` Insert roman ‘\textrm{∗}’ text.  
`C-c C-f C-f` Insert sans serif ‘\textsf{∗}’ text.  
`C-c C-f C-t` Insert typewriter ‘\texttt{∗}’ text.  
`C-c C-f C-c` Insert small caps ‘\textsc{∗}’ text.  
`C-c C-f C-d` Delete the innermost font specification containing pointer.  


### Visual  

AUCTex automatically indents new lines. To fix indentation, press:

`TAB` to reindent the line.  
`M-q` to reindent the paragraph.  
`M-x LaTeX-fill-buffer` to reindent the whole document.  

`C-j` TODO  

`M-x font-lock-mode` Turns off syntax highlighting, which is on by default.  

AUCTex has a folding mode, which hides lots of the syntax of Latex.  

`C-c C-o C-f` Toggle folding mode.  
`C-c C-o C-b` Hide items in buffer.  
`C-c C-o C-r` Hide items in region.  
`C-c C-o C-p` Hide items in paragraph.  
`C-c C-o C-m` Hide current macro.  
`C-c C-o C-e` Hide current environment.  



## Using Latex Generally  

Latex has multiple modes, **paragraph mode**, **math mode**, and **LR mode**. paragraph mode is the default mode for the document environment.  

### Common Environments  

All environments follow the syntax `\begin{NAME} ... \end{NAME}`.  

`quote` Block quote.  

`equation` Math mode for single line, centered and with a label.  
`gather` Math mode for multiple lines, centered.  
`align` Math mode for multiple lines, centered on `&` for each line.  


### Useful Commands

`\noindent` Stops automatic indentation.  
`\verb` (verbatim) Escapes any Latex metacharacters.  
`\texttt` Typewriter font.  

### Math Mode  

`$...$` Text between the dollar signs will be in math mode.  

`\begin{equation} ... \end{equation}` Goes to newline and centers equation with a label.  

`\[...\]` Goes to a newline and centers equation, without a label.

For multiple lines of equations, use the following modes.  

`\begin{gather} ... \end{gather}` Aligns each equation to center.  

`\begin{align} ... \end{align}` Aligns each equation based on where you place a `&` symbol on the line.  

Here are some common commands.

`\frac{x}{y}` Fraction.  
`\dfrac{x}{y}` In-line Fraction.  
`\ge` and `le` Greater than and less than.  
`\int_a^b`, `\iint` Integral and double integral.  
`\sum_{n=1}^\infty` Summation from n=1 to infinity.  


[symbols-manual](https://www.overleaf.com/learn/latex/List_of_Greek_letters_and_math_symbols) contains a list of all math symbols and greek letters.  



## Setting up a Latex Document  

The general syntax for commands in LaTeX is `\command[options]{argument}`.  

All **commands** in Latex start with a `\`. Every documents begins with a `\documentclass` command, with an **argument** in curly braces. The document class loads default styles and look of the document.  

	\documentclass{article}  
	\begin{document}  
	Hello World! % This is a comment!  
	\end{document}  

Some common document classes:  

> `article` For short reports, presentations, articles. The most versatile class.  
> `report` For longer reports.  
> `book` For books.  
> `beamer` For presentations.  


An **environment** changes how a section of text appears, it applies specific typesetting effects.

	\begin{name}  
	The content of the environment is this  
	\end{name}  

A **package** extends the functionality of the language. Packages are applied to a document with the `\usepackage{name}`command, before the `\begin{document}` command.  

> `amsmath` Use of extra math symbols, and features for writing math.  
> `geometry` Set up page geometry, such as setting margins.  
> `float` Allows user to fix placement of figure and table environments.  
> `graphicx` Allows import of external images in many different formats.  
> `enumerate` Allows lists to be enumerated with a variety of characters.  
> `TikZ/PGF` Vector drawing package for high quality figures.  
> `subcaption` Lets multiple in-line floats in a float environment. Must be used with caption package.  


[auctex-manual](https://www.gnu.org/software/auctex/manual/auctex/Quick-Start.html#Quick-Start)  



## In progress

### Vanilla Controls  

`C-c C-o` Insert `\begin` and `\end`, and put the pointer on a line between them.  

`C-c {` Insert ‘{}’ and put pointer between them.  

`C-c }` Go past the next unmatched close brace.  

`"` Inserts quotes.  

> Formatted for Latex. Either ```` after whitespace, `''` after a normal character, or `"` after `\`, `"`, or `C-q`.  


`C-j` Insert paragraph break.  

> Inserts (two newlines) and check the previous paragraph for unbalanced braces or dollar signs.  


`C-c C-e` Close the innermost LaTeX block not yet closed.  

`M-x tex-validate-region` Check each paragraph in the region for unbalanced braces or dollar signs.  



Resources on LaTex in Emacs: [tex-mode-manual](https://www.gnu.org/software/emacs/manual/html_node/emacs/TeX-Mode.html "GNU Tex Mode Manual").  