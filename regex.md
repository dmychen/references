# Regex  

### What is a Regular Expression

A *regular expression* (regex) is a pattern that describes a set of strings. Can use various operators to combine smaller expressions.   

## Grep

We will mostly be using `grep`, which can use three different syntaxes.  

> ERE: extended regular expression.  
> BRE: basic regular expression.  
> PCRE: perl compatible regular expression.  

`grep PATTERN FILE` Searches FILE with the regular expression PATTERN.   

- **`-E`**: Forces ERE to be used.  
* **`-i`**: Ignore case sensitivity.  
* **`-v`**: Invert the match; select non-matching lines.  
* **`-n`**: Print line numbers with each match.  
* **`-c`**: Count the number of matching lines.  
* **`-w`**: Match whole words only.  
* **`-x`**: Match entire lines.  
* **`-q`**: Suppress output.  
* **`-A num`**: Print `num` lines of context after the match.  
* **`-B num`**: Print `num` lines of context before the match.  
* **`-C num`**: Print `num` lines of context before and after the match.  

## Writing Regex  

### Wildcards

**`.`**: matches any one character except a newline.  
- Example: `c.t` matches "cat" or "cot".  

**`*`**: matches zero or more occurences of the preceding character.  
- Example: `ca*t` atches "ct", "cat", or "caat".  

**`+`**: matches one or more occurences of preceding character.  
- Example: `ca+t` matches "cat", "caat", but not "ct".  

**`?`**: matches zero or one occurrence of a character.
- Example: `colou?r` matches "color" and "colour".  
	
**`{n}`**: specifies a number of repetitions of the preceding character.  

> `a{3}` matches "aaa".  
> `{n,}` matches n or more times.  
> `{,n}` matches at most n times.  
> `{n,m}` matches at least n times, no more than m times.  


**`^`**: matches the beginning of a string.  
- Example: `^The` matches "The" if it appears at the start of a string.  


**`$`**: Matches the end of a string.  
- Example: `end$` matches "end" if it appears at the end of a string.  

**`[]`**: Defines a character set. It matches any single character in the list.  

> `[aeiou]` matches any vowel.  
> `[^...]`, `^` at the beginning of the list makes the expression match any character not in the list.  
> `[x-y]` match any character ranging from x to y.  


### Combining Patterns

**`[pattern1]|[pattern2]`** Infix operator. A way of matching two expressions together, that matches strings that matches either  **pattern1** or **pattern2**.  

**Lookaheads** assert a condition is true without consuming any characters.  
`(?=foo)` Positive lookahead. Asserts that foo is matched, but doesn't consume foo.  
- Example: (?=[A-Z])[^AEIOU] // checks for uppercase consonants  
`(?<=foo)` Negative lookahead. Asserts that the following characters do not match foo.  

`()` Form a capturing group.  
`(?:...)` Form a non-capturing group.  

> `\n` Will reference the n-th captured group. 
> `echo "abcdxabcd" | grep -b "\(abc*d\)x\1" # output abcdxabcd`

Multiple regular expressions can be concatenated. Any two concatenated expressions will match strings that is made up of two substrings that respectively match the concatenated expressions.  

The order of precedence in regular expressions is as follows: repetition > concatenation > alternation. 


### Character Classes

**`\c`** Control character  
**`\s`** White space  
**`\S`** Not white space  
**`\d`** Digit  
**`\D`** Not digit  
**`\w`** Word  
**`\W`** Not word  
**`\x`** Hexadecimal digit  
**`\O`** Octal digit  
**`\A`** Start of string  
**`\Z`** End of string  
**`\b`** Word boundary  
**`\B`** Not word boundary  

`[:upper:]` Upper case letters  
`[:lower:]` Lower case letters  
`[:alpha:]` All letters  
`[:alnum:]` Digits and letters  
`[:digit:]` Digits  
`[:xdigit:]` Hexade­cimal digits  
`[:punct:]` Punctuation  
`[:blank:]` Space and tab  
`[:space:]` Blank characters  
`[:cntrl:]` Control characters  
`[:graph:]` Printed characters  
`[:print:]` Printed characters and spaces  
`[:word:]` Digits, letters and underscore  

Practice creating regex expressions at [regex101](https://regex101.com/).  
