# Using YASnippet  

### Using YASnippets  

We can use Yas in `yas-global-mode` and in `yas-minor-mode`.  
 
> To switch to minor mode, first call `yas-reload-all` to load the snippet tables.  

When in minor mode, use snippets by typing the snippet's **trigger key** then typing TAB which cals `yas-expand`. You can also insert a snippet via the keybinding `C-c C-s`. Activating global mode just applies minor mode to all buffers globally.  

`M-x yas-describe-tables` shows a list of available snippets in current mode.  
`M-x yas-new-snippet` creates a template for a new.  
`M-x yas-visit-snippet-file` visits a snippet's definition file, if it exists.  

`C-c C-c` Loads the current snippet being edited to a snippet table, and saves the snippet.  
`C-c C-t` When editing a snippet, opens a new empty buffer to test out the snippet.  

For more information on YASnippet:  

[yasnippet-manual](https://joaotavora.github.io/yasnippet/index.html "Manual")  
[yasnippet-github](https://github.com/joaotavora/yasnippet/blob/master/README.mdown "Yasnippet Github")  
[yasnippet-snippets-github](https://github.com/AndreaCrotti/yasnippet-snippets/blob/master/README.md "Yasnippet official snippets")  
