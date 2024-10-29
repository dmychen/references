# Python

Languages like Bash, Shell, Elisp, Javascript are useful, but it is hard to master all of them. Python is a language that unifies lots of the functionality of all of these languages.  

### Python History  

Larry Wall created python. He designed Perl. Perl tries to mimic natural language, with more than one way of writing the same thing. Many different "dialects" for saying the same thing in Perl, so it can be difficult to understand.  

Python = ABC + Perl - Bad Perl  


Side Note: Google Colab

Very useful! Runs python and can also run bash. Runs a virtual machine, gives you access to a fully fledged file system.  


## Python Language  

### Files

`with open('file.txt', [mode]) as file:` Open a file and manipulate it. **file** represents the file object we can read/write from.  

> `'w'` will write to the file  
> `'a'` will append to the file  
> `'r'` will read from the file  

	with open('myfile.txt', 'r') as f:
	  contents = f.read()
	  new_contents = contents.replace('world', 'universe')
	with open('newfile.txt', 'w') as f:
	  f.write(new_contents)
	  
### Numbers and Strings

**Numbers** can represent integers, floats, complex numbers.  

Operations: +, -, \*, /, %, \*\*.  

**Strings** are immutable when created. We cannot change its value.  

`f"This string contains a magic number, {var}."`. A formatted string. Created by appending **f** to the beginning of the string. Variables can be written in brackets.  


### Lists  

`my_list = [1, 2, 3, 'apple']` Can contain any type. Is mutable.  

> `my_list[2]` can access elements with bracket notation.  

List comprehension  

`list = [operation for x in range]`  

Creates a list, that is initiated with values **x** from a range **range**, which are manipulated with operation **operation**.  

	words = ['hello', 'world', 'python']
	uppercase_words = [word.upper() for word in words]
	
	numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
	even_numbers = [x for x in numbers if x % 2 == 0]
	
	list_of_lists = [[1, 2, 3], [4, 5], [6]]
	flat_list = [item for sublist in list_of_lists for item in sublist]

### Tuples

`my_tuple = (1, 2, 3)` A tuple in Python is immutable.

	squares_tuple = tuple(x**2 for x in range(1, 6))
	
	words = ['apple', 'banana', 'orange']
	word_lengths_tuple = tuple(len(word) for word in words)


### Dictionaries

Dictionaries are like maps in C++. A key is paired with a value. Key-value pairs can be added, removed, or modified. The keys are immutable, but values are mutable.  

	my_dict = {'name': 'Alice', 'age': 30, 'city': 'New York'}
	
Bracket notation can access, modify, or insert a key-value pair.  

	my_dict['age'] = 31
	print(my_dict) 

Can iterate through a dictionary and access both key and value.  

	for key, value in my_dict.items():
		print(key, value)
		
Delete a pair  

	if 'name' in my_dict:
		print("The key 'name' exists in the dictionary.")

Check for existence  

	if 'name' in my_dict:
		print("The key 'name' exists in the dictionary.")
		
### Sets

Sets contain immutable (hashable) items.  

Create a set with `{...}`  

`.add()` Adds an element to a set.  

`.remove()` Removes from a set.  

`.discard()` Removes, doesn't throw error if element isn't present.  

`.union(set2)` Returns union of set1 and set2.  

`.intersection(set2)` Returns intersection of set1 and set2.  

`.difference(set2)` 


### Control Flow  

`for item in list:` For loops will loop through each **item** that is in **list**.  


`foo if (bar)` Equivalent to `if (foo): bar`. Called a ternary operator.  

`if item in foo` Checks for membership in foo.  

`if all(condition for x in foo)` All must fit **condition**  

`if any(condition for x in foo)` Any one item must fit **condition**  

Loop Iterators  

`my_iter = iter(my_list)` Points to data in our list.  


### Yield

`yield VALUE` A function with a yield inside is a generator function. It runs until hitting a yield, and returns that value. When next called it begins after the yield and runs the rest of the function.  
	
	def my_generator(n):
		i = 0
		while i < n:
			yield i
			i += 1
			
	for number in my_generator(5):
		print(number)

### Functions

Can pass arguments by keyword:  

	my_function(arg1=10, arg2="Hi")
	
Pass variable amount of arguments:  

	def my_function(*args):

Pass variable amount of keyword arguments:  

	def my_function(**kwargs):
	
	def my_function(arg1, arg2, *args, **kwargs):
	

Python passes things by object-reference.  

For immutable objects, nothing can change.  

For mutable objects, changes made in function body will change original object. Assignments will not affect original objects, however. You can only change an object in its original address space, can't assign a new value to it!  

