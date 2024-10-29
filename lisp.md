# Emacs Lisp  

### Construction of Emacs  

Core utilities are built with C.  
Higher level abstraction on top built with Lisp. Also Object Oriented.  

There are many possiblities for customizing the behavior of emacs with Lisp.  

`foo.el` Lisp files end in .el.  

Lisp is called a *small language*. It has an intepreter that reads and executes Elisp code.  

It is a functional language.  

### Basic Syntax  

Elisp is built out of Atoms (numbers, strings, symbols) and Lists (ordered collection of elements).  

`(op arg1 arg2)` Symbolic expressions are written in prefix notation.  

> one way to visualize this expression is as a function. **op** is the function call and **arg1** and **arg2** are the arguments to that function.  
> (+ 1 1) ==> 1+1=2  

Some variables in Lisp:  
`30` Is a number literal  
`#b111` Binary  
`#bx111` Hexdadecimal  
`"Hello"` String  
`nil` or `()` False  
`t` True  

#### Expressions

`(setq my-variable 20)` Define/set a variable.  
- Example: (setq my-variable 20)  

`(if (condition) (then) (else))` If statements.  
- Example: (if (> 3 2) (print "3 is greater than 2") (print "3 is not greater than 2"))  

`(cond (condition) (then) (condition) (then) (else))` Use `Cond` if you have multiple conditions.  

`(while (condition) (body))` While statements.  

> (setq i 1)  
> (while (<= i 10) (print i) (setq i (+ 1 i)));  

`(dotimes (i 5) (message "Iteration: %d" i))` A dotimes looping construction.  

`(dolist (element some-list)` Loops for each element in some-list.  

`(defun function-name (param1 param2) expression1 expression2 )` Create a function.  

`(function-name arg1 arg2 arg3)` Call a function.  

> The return value for a function is the last expression executed by the function.  

`(condition-case nil (my-function) (error (message "An error occurred.")))` Handles errors.  

Hooks and Advice: Elisp supports hooks (functions run at certain points) and advice (modifying the behavior of existing functions). Hooks are defined with add-hook.  

### Customizing Emacs

#### Manipulating Pointer

`backward-char`: Moves point backward one character.  
`forward-char`: Moves point forward one character.  
`beginning-of-line`: Moves point to the beginning of the line.  
`end-of-line`: Moves point to the end of the line.  


`point`: Returns the current position of point.  
`point-min`: Returns the beginning of the buffer.  
`goto-char`: Moves point to a specific position.  
- Example: (goto-char (point-min)) moves point to beginning of buffer.  

#### Insertion

`insert-char`: Inserts a single character at point.  
`delete-char`: Deletes the character at point.  
`kill-line`: Deletes the current line.  
`yank`: Pastes the last killed text.  

`message`: Displays a message in the minibuffer.  
- Usage (message FORMAT &rest ARG)  
- Example: (message "Hello, Emacs!")  
- Example: (message "Hello, %s!" "World")  

`insert`: Inserts text at point. It can be used to insert strings, numbers, or the results of expressions.  
- Example: (insert "Hello, world!")

`format`: Formats a string according to a format string. Similar to printf in C.
- Example: (format "The value of pi is approximately %f" pi)

#### Strings

`make-string` Creates a string of given length filled with a specific character.  
- Usage: (make-string length char)  
- Example: (make-string 10 ?*) // Creates a string of 10 asterisks  
  - the `?` specifies that `*` is a character not a string.  

`string` Converts an object to a string representation.  
- Usage: (string object)  
- Example: (string 123) // Converts the number 123 to the string "123"

`substring` Extracts a substring from a string.  
- Usage: (substring string start end)  
- Example: (substring "Hello, world!" 7) // Extracts "world!"

`concat` Concatenates multiple strings.  
- Usage: (concat string1 string2 ...)  
- Example: (concat "Hello, " "world!") // Concatenates the strings to "Hello, world!"
- Example: (concat (make-string 5 "Hello")) // "HelloHelloHelloHelloHello"

`format-time-string` Formats current time according to format string.  
- Usage: (format-time-string FORMAT &optional TIME)  
- Example: (format-time-string "%Y-%m-%d %H:%M:%S") -> "2024-10-25 12:30:45"  

> %Y: Four-digit year (e.g., 2024)  
> %y: Two-digit year (e.g., 24)  
> %m: Two-digit month (01 to 12)  
> %B: Full month name (e.g., October)  
> %b or %h: Abbreviated month name (e.g., Oct)  
> %d: Two-digit day of the month (01 to 31)  
> %e: Day of the month (1 to 31, without leading zero)  
> %j: Day of the year (001 to 366)  
> %A: Full weekday name (e.g., Friday)  
> %a: Abbreviated weekday name (e.g., Fri)  
> %u: Day of the week (1 to 7, where Monday is 1)  
> %H: Hour (00 to 23)  
> %I: Hour (01 to 12)  
> %M: Minute (00 to 59)  
> %S: Second (00 to 59)  
> %p: AM or PM designation  

`insert-date` Inserts current date into buffer. Usually used in conjunction with format-time-string.  

#### Interaction

`interactive` Makes a function that can be called interactively by users. Can take user input. Specify different types of input using prefixes.
- Example: (interactive "sEnter text: ") // takes a string input.  
- Other prefixes: `n` number. `f` file. `D` directory. etc...  

`global-set-key`: Sets a global key binding.  
- Usagee: (global-set-key (kbd "key-binding:) `command-name)  
- Alt: M-x global-set-key RET key-binding command-name RET  
- Example: (global-set-key (kbd "C-c C-h") 'my-hello-world)  

#### Testing

`(require 'ert)` Loads the ert library, Emac's lisp testing framework. 
`ert-deftest` Macro that creates a new test function.  
`should` Used to say enclosed assertion must evaluate to true for the test to pass.  
`M-x ert RET test-function RET` Allows you to run test-function.  

Usage: `(ert-deftest some-test () (should (assertion-here)))`
Example: ('require ert) (ert-deftest sum-evens-test () (should (= (sum-evens '(1 3 5)) 0 )) (should (= (sum-evens '(2 4 6)) 12)))  


### Examples

Create interactive function:  

	(defun my-interactive-function (arg1 arg2 arg3)
	  (interactive "sString argument: \niInteger argument: \nxFile name: ")
	  (message "You entered: %s %d %s" arg1 arg2 arg3))

  
Count words in buffer:  

	(defun count-words ()
	  (interactive)
	  (let ((words 0))
	    (goto-char (point-min))
		(while (forward-word)
		  (setq words (+ 1 words))
		  )
	    (message (format "Words in Buffer: %s" words))))

Display current line / number of lines in buffer:  

	(defun gps-line ()
	  "Print the current buffer line number and narrowed line number of point."
	  (interactive)
	  (let ((start (point-min))
		(n (line-number-at-pos))
		(count 0))
		(save-excursion   ;; Save cursor position
		  (goto-char (point-min))
		  (while (re-search-forward (regexp-quote "\n") nil t) ;; look for newlines
			(setq count (1+ count))))
		(if (= start 1)
		(message "Line %d/%d" n count)
		  (save-excursion
		(save-restriction
		  (widen)
		  (message "line %d/%d"
		    (+ n (line-number-at-pos start) -1) count))))))
