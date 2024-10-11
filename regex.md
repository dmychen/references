# Regex  

### What is a Regular Expression

A *regular expression* (regex) is a pattern that describes a set of strings. Can use various operators to combine smaller expressions.   

We will be using `grep`, which can use three different syntaxes.  

> ERE: extended regular expression.  
> BRE: basic regular expression.  
> PCRE: perl compatible regular expression.  


### Grep

`grep PATTERN FILE` Searches FILE with the regular expression PATTERN.   

> `-E` Forces ERE to be used.  

`sed s/PATTERN1/PATTERN2/g`  idk its confusing. Basically find and replace.


### Metacharacters  

ERE uses metacharacters to match patterns.  

`.` matches any one character except a newline.  

> `c.t` matches "cat" or "cot".  


`*` matches zero or more occurences of the preceding character.  

> `ca*t` atches "ct", "cat", or "caat".  


`+` matches one or more occurences of preceding character.  

> `ca+t` matches "cat", "caat", but not "ct".  


`?` matches zero or one occurrence of a character.

> `colou?r` matches "color" and "colour".  


`{n}` specifies a number of repetitions of the preceding character.  

> `a{3}` matches "aaa".  
> `{n,}` matches n or more times.  
> `{,n}` matches at most n times.  
> `{n,m}` matches at least n times, no more than m times.  


`^` matches the beginning of a string.  

> `^The` matches "The" if it appears at the start of a string.  


`$` Matches the end of a string.  

> `end$` matches "end" if it appears at the end of a string.  

`[]` Defines a character set. It matches any single character in the list.  

> `[aeiou]` matches any vowel.  
>   
> `[^...]`, if `^` appears at the beginning of the list, makes the expression match any character not in the list.  
> `[x-y]` makes the expression match any character ranging from x to y.  


`[pattern1]|[pattern2]` Or operator. Matches either **pattern1** or **pattern2**.  

`[pattern](?=foo)` Positive lookahead. Only matches **pattern** if it's followed by **foo**.  

`(?<=foo)[pattern]` Negative lookahead. Only matches **pattern** if it comes after **foo**.  



Multiple regular expressions can be concatenated. Any two concatenated expressions will match strings that is made up of two substrings that respectively match the concatenated expressions.  

Multiple regular expressions can be joined together with the `|` infix operator. The resulting expression matches any string that matches either of the expressions.  

The order of precedence in regular expressions is as follows: repetition > concatenation > alternation. Use `()` to override precedence rules and form a subexpression.  


Practice creating regex expressions at [regex101](https://regex101.com/).  
