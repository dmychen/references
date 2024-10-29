# Python

## Syntax

### File I/O

**`with open(filename, mode) as file_object:`**	Opens a file in the specified mode ('r', 'w', 'a', 'x') and assigns it to file_object.  

`file_object.read()`	Reads the entire content of the file as a string.  
`file_object.readline(`)	Reads a single line from the file.  
`file_object.readlines()`	Reads all lines from the file and returns them as a list of strings.  
`file_object.write(string)`	Writes the given string to the file.  
`file_object.writelines(list_of_strings)`	Writes a list of strings to the file.  
`file_object.close()`	Closes the file (usually handled automatically by with open).  

###  Data Types

Immutable types are typically hashable.  
Mutable types: Lists, Dictionaries, Sets.  
Immutable types: Integers, Floats, Strings, Tuples, Bools, Frozensets.  

**`int(value)`**	Converts a value to an integer.  

**`float(value)`**	Converts a value to a floating-point number.  

**`str(value)`**	Converts a value to a string.  

**`list(iterable)`**	Creates a list from an iterable (e.g., a string, tuple, or range).  

`[expression for item in iterable if condition]`	List comprehension for creating lists.  

**`tuple(iterable)`**	Creates a tuple from an iterable.  

**`dict(iterable)`**	Creates a dictionary from an iterable of key-value pairs.   

> Can iterate over keys, values, or key-value pairs using .keys(), .values(), or .items()

    my_dict = {'key1': 'value1', 'key2': 'value2'}  
    my_dict = dict(key1='value1', key2='value2')  
	
**`set(iterable)`**	Creates a set from an iterable.  

> `.add()` Adds an element to a set.  
> `.remove()` Removes from a set.  
> `.discard()` Removes, doesn't throw error if element isn't present.  
> `.union(set2)` Returns union of set1 and set2.  
> `.intersection(set2)` Returns intersection of set1 and set2.  
> `.difference(set2)` 

**`bool(value)`**	Converts a value to a boolean (True or False).  


### Control Flow

**`if condition:`**	Executes a block of code if the condition is True.  

**`expression_if_true if condition else expression_if_false`**	Ternary operator for concise if/else statements.  

**`elif condition:`**	Executes a block of code if the preceding if or elif condition was False and this condition is True.  

**`else:`**	Executes a block of code if all preceding if and elif conditions were False.  

**`for variable in iterable:`**	Iterates over the elements of an iterable.  

**`while condition:`**	Executes a block of code as long as the condition is True.  

**`break`**	Exits the current loop.  

**`continue`**	Skips the rest of the current iteration and proceeds to the next.  


### Functions

**`def function_name(parameters=default):`** Defines a function with the given name and parameters.  

> `def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):` Creates a function with positional arguments before the `/`, either positional or keyword arguments in the middle, and only keyword arguments following the `*`.  
> `*args` A parameter that accepts a variable number of positional argumentes into a tuple.   
> `**kwargs` An parameter that accepts a variable number of keyword arguments into a dictionary.  
> When an argument is already a tuple/dictionary, the opposite occurs: \*tup unpacks a tuple tup, and \*\*dict unpacks a dictionary dict

`return value`	Returns a value from the function.  
`function_name(arguments)`	Calls the function with the given arguments.  
`lambda parameters: expression`	Creates an anonymous function (lambda function).  

    # Anonymous Function Example  
    square = lambda x: x * x  
    print(square(5))  # Output: 25  


### Generators (Yield)

**`yield VALUE`** A function with a yield inside is a generator function. It runs until hitting a yield, and returns that value. When next called it begins after the yield and runs the rest of the function.  
- *Yield allows you to iterate without storing an entire sequence in memory.*  
- A generator function **retains state** between calls. Resumes where it ended.  
- Can have multiple yields.  
	
	def my_generator(n):
		i = 0
		while i < n:
			yield i
			i += 1
			
	for number in my_generator(5):
		print(number)


### Classes (OOP)

**`class ClassName:`**	Defines a class.  

`__init__(self, parameters)`	Constructor method, called when an object of the class is created.  
`self.attribute_name = value`	Assigns a value to an attribute of the object.  
`def method_name(self, parameters):`	Defines a method within the class.  
`object = ClassName(arguments)`	Creates an object of the class.  
`object.method_name(arguments)`	Calls a method of the object.  


#### Class Properties

**`__name__`**: The name of the class as a string.  
`__module__`: The name of the module in which the class was defined.  
**`__dict__`**: A dictionary containing an class or an instance's writable attributes/methods and values.  
`__bases__`: A tuple containing the base classes (superclasses) of the class.  
**`__init__`**: The constructor method for initializing new objects of the class.  
`__str__`: A method that returns a user-friendly string representation of the class.  
`__class__`: A reference to the class of the instance (used in instance methods).  
`__doc__`: The documentation string for the class.  
`__annotations__`: A dictionary containing type annotations for the class attributes and methods.  
`__slots__`: If defined, this property restricts attribute creation, optimizing memory usage.  
`__setattr__`: A method that defines behavior for setting attributes.  
`__getattr__`: A method that defines behavior for getting attributes that don’t exist.  
`__delattr__`: A method that defines behavior for deleting attributes.  
`__hash__`: A method that returns the hash value of the class instance (if applicable).  

Special Methods: (Dunder Methods)  

`__eq__`, `__ne__`: Define behavior for equality and inequality comparisons.
`__lt__`, `__le__`, `__gt__`, `__ge__`: Define behavior for comparison operations.
`__add__`, `__sub__`, etc.: Define behavior for arithmetic operations.
`__len__`: Defines behavior for the built-in len() functio

#### Class Example

	class MyClass:
		class_attribute = 10 # An attribute shared among instances of this class

		def __init__(self, name):
			self.name = name # Each instance has a unique attribute

	print(obj.__dict__)  # Output: {'name': 'Alice'}
	
	print(MyClass.__dict__) # {'__module__': '__main__', 'class_attribute': 10, '__init__': <function MyClass.__init__ at 0x7f8b23459ee0>}


### Miscellaneous

#### Error Handling

`try:`	Encloses the code that might raise an exception.  
`except ExceptionType as variable_name:`	Specifies the type of exception to catch and the code to handle it.  
`else:`	Executes if no exception occurs in the try block.  
`finally:`	Executes regardless of whether an exception occurred or not.  

#### Scripting

`if __name__ == "__main__": main()` Checks is script is being run as main program. If not, won't execute automatically

#### Garbage

Python uses reference counting to garbage collect. If an object's reference count = 0, deallocates it.  


## Modules and Packages

`import module_name`	Imports a module.  
`from module_name import function_name`	Imports a specific function from a module.  
`from module_name import *`	Imports all functions and variables from a module (generally not recommended).  
`module_name.function_name()`	Calls a function from the imported module.  

### sys

Provides access to system-specific parameters and functions. Can be used to manipulate Python's runtime environment.  

`sys.argv` A list containing command-line arguments passed to the script. sys.argv[0] is the script name.  
`sys.version`: A string containing the version of the Python interpreter being used.
`sys.platform`: A string indicating the platform (e.g., 'win32', 'linux', 'darwin').
`sys.path`: A list of strings that specifies the search path for modules. It can be modified to include additional directories.
`sys.modules`: A dictionary of all imported modules. Maps module names (strings) to module objects in memory. 

`sys.exit(code)` Exits the script with the specified exit code (0 for successful termination).  

IO: 

`sys.stdin` Standard input (usually the keyboard).  
`sys.stdout` Standard output (usually the console).  
`sys.stderr` Standard error  


### random

Generates random numbers and random operations. Import with `python import random`.  

`random.random()` Generates a random float number between 0.0 (inclusive) and 1.0 (exclusive).  
> Use `random.uniform(a, b)` to specify a range for random float.  

`random.randint(a, b)` Generates a random integer between a (inclusive) and b (inclusive).  

`random.choice(sequence)` Returns a random element from the given sequence. Can be a list or tuple.  

`random.sample(population, k)` Returns a list of `k` unique elements from `population`.  

`random.shuffle(x)` Shuffles `x` in place. Order of elements is randomly rearranged.  



### argparse

**Purpose:**  
- Parses command-line arguments.  
- Defines how users can interact with your script via the command line.  

* **`ArgumentParser()`:**  
  - `description`: A brief description of the script.  
  - `usage`: How to use the script.  
  - `prog`: The name of the program.  
  - `epilog`: Text printed after the argument help.  
  - `add_help`: Whether to include a -h/--help option.  

* **`add_argument()`:**  
  - `name or flags`: One or more names for the argument.  
  - `nargs`: Number of command-line arguments that should be consumed.  
	- `?`: Zero or one argument.  
	- `*`: Zero or more arguments, stored as a list.  
	- `+`: One or more arguments, stored as a list.  
  - `type`: The type of the argument. Can be a function that returns a string  
  - `default`: Default value if the argument is not provided.  
  - `choices`: A list of valid choices for the argument.  
  - `required`: Whether the argument is required.  
  - `help`: A help message for the argument.  
  - `metavar`: A metavariable name for the argument in help messages.
  - `action`: The basic type of action to be taken when this argument is encountered at the command line.  
	- `store`: Store the argument's value.  
	- `store_const`: Store a constant value.  
	- `store_true`: Store `True` if the flag is present, `False` otherwise.  
	- `store_false`: Store `False` if the flag is present, `True` otherwise.  


* **`append`:** Append values to a list.  
* **`append_const`:** Append a constant value to a list.  
* **`count`:** Count the number of times the argument occurs.  

	\# Simple Example:
	import argparse

	parser = argparse.ArgumentParser(description='Process some integers.')
	parser.add_argument('integers', metavar='N', type=int, nargs='+',
					   help='an integer for the accumulator')
	parser.add_argument('--sum', dest='accumulate', action='store_const',
					   const=sum, default=max,
					   help='sum the integers (default: find the max)')

	args = parser.parse_args()

	print(args.accumulate(args.integers))


## Code examples

#### Assignment 2:  

	#!/usr/bin/python
	"""
	Outputs a random permutation of its input lines.
	"""

	import random, sys, argparse

	# --input-range should have the form [int]-[int]
	def format_range(str):
		# split string around '-'
		left, right = str.split('-', 1)
		# check if the string is an int, and range is valid
		try:
			left = int(left)
			right = int(right)
			if left > right:
				raise argparse.ArgumentTypeError(f"Invalid range format: {left}-{right}")
			return left, right
		# othewise throw a type/value error
		except (ValueError, TypeError):
			raise argparse.ArgumentTypeError(f"Invalid range format: {left}-{right}")

	def main():
		# Help messages
		usage_msg = """%(prog)s [OPTION]... FILE
	Outputs a random permutation of its input lines"""
		echo_help_msg = ""

		# Create an argument parser.
		parser = argparse.ArgumentParser(usage=usage_msg)
		# Create arguments
		parser.add_argument('-e', '--echo', action='store', nargs='*', dest='echo', help=echo_help_msg)
		parser.add_argument('-i', '--input-range', action='store', type=format_range, nargs=1, dest='range', help="-i")
		parser.add_argument('-n', '--head-count', action='store', type=int, nargs=1, dest='count', help="-n")
		parser.add_argument('-r', '--repeat', action='store_true', dest='repeat', help="-r")
		parser.add_argument('filename', type=str, nargs='?', default='-', help="The name of the input file")
		# Read parsed arguments into args
		args = parser.parse_args(sys.argv[1:])

		# create a list with appropriate lines from the input
		lines = []
		# if -i, set list to range of numbers
		if args.range is not None:
			start, end = args.range[0]
			numbers = list(range(start, end+1))
			lines = [str(num) + '\n' for num in numbers]
		# or if -e, set list to CLI arguments
		elif args.echo is not None:
			lines = [line + '\n' for line in args.echo]
		# or if no input file, read from stdin
		elif args.filename == '-':
			lines = [line for line in sys.stdin]
		# otherwise read from an input file
		else:
		   with open(args.filename, 'r') as file:
				lines = file.readlines()

		count = -1
		if args.count is not None:
			count = args.count[0]

		# if -r, we print from lines with replacement
		if args.repeat:
			if lines:
				while count != 0:
					sys.stdout.write(random.choice(lines))
					count = count - 1

		# otherwise shuffle lines and print
		new_lines = []
		for line in lines:
			if count == 0:
				break
			new_lines.append(line)
			count = count - 1
			# randomly shuffle the lines
		random.shuffle(new_lines)
			# output lines in list
		for line in new_lines:
			s = str(line)
			sys.stdout.write(s)

	if __name__ == "__main__":
		main()

#### Random Number Guesser

	\#!/usr/bin/env python3
	import argparse, random, sys

	parser = argparse.ArgumentParser(“shuf”)
	parser.add_argument(“-r”, “--range”, type=str)
	parser.add_argument(“-t, “--tries”, type=int)

	args = vars(parser.parse_args())

	range_option = args.get(“range”)
	tries_option = args.get(“tries”)

	if not range_option:
		 sys.stderr.write(“-r flag is required\n”)
		 sys.exit(1)

	[start, end] = [int(opt) for opt in range_option.split(“-”)]


	numbers = [i for i in range(start, end + 1)]

	tries = 1
	if tries_option:
		 tries = tries_option

	while tries > 0:
		 answer = random.choice(numbers)
		 guess = input(“>”)
		 if int(guess) == answer:
			  sys.stdout.write(“Yay you win :)\n”)
			  break
		 else:
			  if tries_option:
					sys.stdout.write(“Wrong you fail :(“)
			  else:
					 sys.stdout.write(“Nope\n”)
		 tries -= 1



# Linux and Files

#### Files:  

A collection of data stored on a disk, that represents information. Can be a document, image, video, executable program, etc...  
- **Properties**: Each file has attributes. Name, Inode (see "Linking"), Content (data).  

#### Directories  

Directories contain other files and directories. It contains multiple directory entries, each corresponding to files or subdirectories. Every directory is itself a directory entry.  
- **Hard Linking**: A directory can contain multiple entries pointing to one inode.  

- `/`: Root directory.  
- `/bin`: Essential command binaries.  
- `/etc`: Configuration files.  
- `/home`: User home directories.  
- `/lib`: Essential shared libraries.  
- `/tmp`: Temporary files.  
- `/usr`: User utilities and applications.  
- `/var`: Variable data files (logs, databases).  


**Directory Entry**  

A record within a directory that associates a filename with its corresponding inode. Acts as a link between the filename and file's metadata.  
- Filename, file size, permissions, ownership, timestamps, inode number.  

#### Globbing Characters (Wildcards):  

- `*`	Matches zero or more characters.  
  - *.txt (matches all .txt files)  
- `?`	Matches exactly one character.  
  - file?.txt (matches file1.txt)  
- `[...]` Matches any single character within brackets.  
  - file[abc].txt, m[a,o,u]m, m[a-d]m  
- `{...}` Matches any terms separated by commas.  
- `!` or `^` inside `[...]`	Excludes characters in the set.  
  - file[!abc].txt (matches files not ending in a, b, or c)  
- `~`	Represents the current user's home directory.  
  - ~/documents (refers to /home/user/documents)  
- `.`	Represents the current directory or indicates hidden files.  
  - ./script.sh (refers to script.sh in the current directory)  
- `..`	Represents the parent directory.  
  - ../file.txt (refers to file.txt in the parent directory)  
- `**`	Matches directories recursively (in some shells)  
  - \*\*/\*.txt (matches all .txt files in current and subdirectories)  

### Piping and Redirection

**Standard Input (stdin)**: Input stream (default is keyboard).  
**Standard Output (stdout)**: Output stream (default is terminal).  
**Standard Error (stderr)**: Error output stream (default is terminal).  

#### Redirection

- `>`: Redirect stdout to a file (overwrite).  
  - Example: echo "Hello, World!" > output.txt  
- `>>`: Append stdout to a file.  
  - Example: echo "Another line" >> output.txt  
- `<`: Redirect stdin from a file.  
  - Example: sort < input.txt  
- `2>`: Redirect stderr to a file (overwrite).  
  - Example: command_that_fails 2> error.log  
- `2>>`: Append stderr to a file.  
  - Example: command_that_fails 2>> error.log  
- `&>`: Redirect both stdout and stderr to a file (overwrite).  
  - Example: command &> all_output.log  
- `&>>`: Append both stdout and stderr to a file.  
  - Example: command &>> all_output.log  
- `2>&1` Sends stderr into whatever output stdout is going to.  
  - Example: command > output.txt 2>&1 (sends stdout to output.txt, then stderr also)  
	- command 2>&1 > output.txt (sends stderr to terminal, stdout to ouput.txt)  
- `<&0` Duplicate standard input (Redirects stdin to itself)

Using `>` will overwrite an existing file without warning. Use `>>` to append.  
Permissions: Ensure you have permission to write to the target file.  
Non-existent Files: Redirecting to a non-existent file will create it automatically.  

#### Piping

`|` Allows you to send the stdout of one command as the input of another.  
- Example: cat file.txt | sort | uniq -c | sort -nr  

Buffering: Piping may introduce buffering delays. Commands may not execute until the buffer is full.  
Exit Status: The exit status of a pipeline is the exit status of the last command in the pipeline.  


### Important Commands

**`ls [options] [file...]`** List directory contents.  
- `-a`: Show all files, including hidden files (those starting with `.`).  
- `-l`: Use a long listing format (detailed information).  
- `-h`: Human-readable sizes (used with `-l`).  
- `-R`: Recursively list subdirectories.  
- `-t`: Sort by modification time.  
- `-i`: Show inode info  
  
**`ln [options] <target> [<link_name>]`** Create links.  
- Creates links (see "Linking"). If a hard link already exists with the specified target name, command fails.  
- `-s`: Create a symbolic link instead of a hard link.  
  - If `<target>` contains a full path, it will create an absolute symlink.  
	- Example: ln -s /home/user/documents/report.txt report-link  
  - If `<target>` contains a relative path or just a file name, it will create a relative symlink.  
  - If a symlink already exists with the specified target name, command fails.  
  - **Example**: ln -s config.txt my_config  
- `-f`: Remove existing destination files.  
- `-n`: Treat the destination as a normal file if it is a directory.  

**`chmod [options] mode file...`** Change file modes or access control lists.  
- `-R`: Apply changes recursively to directories and their contents.  
- `-v`: Verbose  
- Owner (u): Single person considered primary owner of the file.  
- Group (g): Connected to the file in some way, but not as much as the owner.  
- Other (o): Anyone else.  
- Mode syntax:  
  - Numeric: chmod 755 file.txt  
  - Symbolic: chmod u+x file.txt  
  
**`rm [options] [file...]`** Remove files and directories.  
- `-r`: Remove directories and their contents recursively.  
- `-f`: Force removal without prompting.  
- `-i`: Prompt before each removal.  

**`cp [options] <source> <destination>`** Copy files and directories.  
- Creates a new file, or overwrites existing file.  
- `-r`: Copy directories recursively.  
- `-i`: Prompt before overwriting files.  
- `-u`: Copy only when the source file is newer than the destination file or when the destination file is missing.  
- `-v`: Verbose; show files being copied.  

### Complex Commands

#### **`find [path...] [expression]`** 

Recursively descends the directory tree for each path listed, evaluating an expression (composed of the “primaries” and “operands” listed below) in terms of each file in the tree.  

**Options**:
- `-name <pattern>`: Search for files matching a specific pattern (case-sensitive).  
  - Example: `find . -name "*.txt"`  
- `-iname <pattern>`: Search for files matching a pattern (case-insensitive).  
  - Example: `find . -iname "*.txt"`  
- `-type <type>`: Specify the type of file to find:  
  - `f`: Regular file, `d`: Directory, `l`: Symbolic link  
  - Example: `find . -type d`  
- `-size <n>`: Find files of a specific size.  
  - Use `k` for kilobytes, `M` for megabytes, `G` for gigabytes.  
  - Example: `find . -size +10M` (larger than 10 MB)  
- `-mtime <n>`: Find files modified n days ago.  
  - Use `+` for more than, `-` for less than.  
  - Example: `find . -mtime -7` (modified in the last 7 days)  
- `-atime <n>`: Find files accessed n days ago.  
- `-ctime <n>`: Find files changed n days ago (i.e., status change).  
- `-maxdepth <n>`: Limit the search to n levels of directories.  
  - Example: `find . -maxdepth 2 -name "*.txt"`  
- `-mindepth <n>`: Skip the first n levels of directories in the search.  
**Logical Operators**:  
- `-and`: Combine multiple conditions (default).  
  - Example: `find . -type f -and -size +1M`  
- `-or`: Combine conditions; either condition can be true.  
  - Example: `find . -name "*.jpg" -or -name "*.png"`  
- `-not`: Negate a condition.  
  - Example: `find . -not -name "*.txt"`  
**Actions**:  
- `-print`: Output the found files (default action).    
- `-exec <command> {}`: Execute a command on each found file.  
  - Use `\;` to terminate the command.  
  - Example: `find . -type f -exec chmod 644 {} \;`  
- `-execdir <command> {}`: Similar to `-exec`, but runs the command from the directory where the file was found.  
- `-delete`: Delete the found files.  
  - Example: `find . -type f -name "*.tmp" -delete`  

#### **`sed [options] 'script' [input_file]`** 

Text substitution, deletion, insertion, transformation.  

**Options**:  
- `e`: Specify a command to be executed.  
  - `sed -e 's/foo/bar/g' -e 's/baz/qux/g' file.txt`  
- i[SUFFIX]: Edit files in place; if a suffix is provided, backup files are created.  
  - `sed -i.bak 's/old/new/g' file.txt  # Creates file.txt.bak`  
- n: Suppress automatic output; only output lines explicitly specified with p.  
- r or -E: Use extended regular expressions.  
  - `sed -E 's/(foo|bar)/baz/g' file.txt`  
**Commands**:  
- **`p`:** Print the current pattern space.  
  - `sed -n '1,3p' file.txt`  Print lines 1 to 3  
- **`d`:** Delete the current pattern space.  
  - `sed '2d' file.txt` Deletes the second line  
  - `sed '/pattern/d' file.txt` Deletes lines matching 'pattern'  
- **`s/pattern/replacement/flags`:** Substitute `pattern` with `replacement`.  
  - `g`: Replace all occurrences in a line.  
	- `sed 's/old/new/g'` file.txt  
	- `i`: Case-insensitive substitution.  
- **`a\text`:** Append text after the current line.
- **`i\text`:** Insert text before the current line.
- **`c\text`:** Replace the current line with text.
  - `sed '/pattern/c\New Line' file.txt`  
  
#### **`sort [input_file]`**

Sort lines in a text file.  

- `-r`: Sort in reverse order.  
- `-n`: Sort by numerical value.  
- `-k`: Specify a key (column) to sort by (e.g., -k2 to sort by the second column).  
- `-u`: suppress repeated lines.  
- `-o FILE`: Write output to a file instead of stdout  

#### **`tr [options] SET1 SET2`**

Used to translate or delete characters.  

- `-d`: Delete characters in SET1. (no set 2)  
- `-s`: Squeeze repeated characters.  
- `-c`: Complement the character set.  
- Example: tr 'a-z' 'A-Z' < input.txt > output.txt  z

#### **`comm [options] file1 file2`**

Compare two sorted files line by line.  

- `-1`, `-2`, `-3`: Suppress lines unique to file1, file2, or both.  

#### **`awk 'pattern { action }' file`**

Pattern scanning and processing. Good for workign with structured data.  

- **pattern**: condition to determin whether action is executed.  
- **action**: command to be executed.  
  - `\$n` can specify the nth field of each line (space-separated by default)  
  - ie: `awk -F, '{ print \$1, \$3 }' file.txt`  
- `-F` set field-separator to be the following regex.  
- Use regex by creating a pattern of form `'/.../`. The `'` stops shell from interpreting special characters, passing it directly to regex.  

> Example of combining commands: `tr -cs "A-Za-z0-9,'\.!/-" "[\n*]" | sort -u | comm -23 - sorted.word`
  
### Linking
	
#### Inodes  
An inode (index node) is a data structure that stores metadata about a file or directory, including its attributes (size, permissions, timestamps) and the location of its data blocks. Each file has a unique **inode number** and a **link count**.  
- For regular files, the link count is the number of hard Links.  
- For directories, it's the count of the directory itself plus the subdirectories.  
- For symbolic links, it's always 1, since symbolic links do not affect the link count of their target.  

#### Hard Links  
- **Inode**: Both the original file and the hard link share the same inode number. The operating system cannot differentiate between the original file and its hard links.
- **Mutual Updates**: Changes made to one file (e.g., modifying content) affect the other because they reference the same data.  
- **Deletion**: When a hard link is deleted, the inode's reference count decreases. The file is only actually deleted when the reference count drops to zero (i.e., all hard links are removed).  
- **Limitations**: Cannot create hard links to directories (to prevent cycles) or across different filesystems.  

#### Symlinks  
- **Definition**: A symbolic link is a pointer to a pathname, acting as a shortcut to another file or directory.  
- **Different Inode**: Symlinks have their own inode and point to the pathname of the target. Does not effect reference number of target file.  
- **Independent**: Modifying or deleting a symlink does not affect the original file or directory
- **Benefits** Space efficiency: Links take up minimal space compared to copying large files/directories. Easier than navigating long paths.  


### Processes

A process is an instance of a running program. Each has its own memory space and system resources.  
- **Process ID (PID)**: A unique identifier assigned to each process.  
- **Parent Process ID (PPID)**: The PID of the process that started (or spawned) the current process.  
- **State**: Processes can be in different states, such as running, sleeping, stopped, or zombie.  
- **Foreground and Background Processes**: Foreground processes interact with the terminal, while background processes run without user interaction.  

`ps [options]` Display information about active processes.   

- `ps`: Displays processes running in the current shell.  
   - Example: ps  

- `-e` or `-A`: Displays all processes running on the system.  
   - Example: ps -e  

- `-f`: Provides a full-format listing, showing more details like the user, PID, PPID, and command.  
   - Example: ps -ef  

- `-u <user>`: Displays processes for a specific user.  
   - Example: ps -u username  

- `-p <pid>`: Displays information for a specific PID.  
   - Example: ps -p 1234  

- `--sort <key>`: Sorts the output based on specified criteria (e.g., `%cpu`, `%mem`).  
   - Example: ps --sort=-%mem  

- `-l`: Displays a long format that includes additional information like the process state and priority.  
   - Example: ps -l  
   
- `ps aux (BSD/macOS style)`: This is a common combination of options that
provides a very comprehensive process listing. `a` lists processes of all
users, `u` provides user-oriented output, and `x` includes processes without
a controlling terminal.  
   
Potential output fields include:  
- **PID**: Process ID.  
- **TTY**: Terminal associated with the process.  
- **TIME**: CPU time used by the process.  
- **CMD**: Command that started the process.  
- **USER**: User who owns the process.  
- **%CPU**: Percentage of CPU usage.  
- **%MEM**: Percentage of memory usage.  

`kill PID` Kills a process.  
`kill -9 PID` Forcefully kills a process.  

# Bash Scripting

A bash script is named `name.sh`. Run with `bash name.sh`.  
First line should be: `#!/bin/bash`. A shebang that specifies the interpreter.  



**Variables**  

`NAME=value` No spaces around the equals.  
`${NAME}` Accesses the variable.  

**Arguments**  
`$n` Refers to the nth parameter of the script.  
- ie: `$0` refers to name of script.  
`$#` Number of arguments  
`$$` Process ID.  

**Strings**  
if `name="John"`  
`echo "Hi $name"` Prints "Hi John".  
`echo 'Hi $name'` Prints "Hi $name".  

**Functions**  

`func_name () { ... }` Declare a function.  
`func_name` Calls the function. Don't need `()` if no params.  

**Conditionals**  

`if [[condition]]; then ...` If condition is true, evaluate then.  
`elif [[condition]]; then ...` Otherwise evaluate the elif.  
`fi` Marks end of conditional.  
- `[[NUM cond NUM]]` Compare integers. `-eq`, `-ne`, `-lt`, `-gt`, `ge`.  
- `[[cond STR]]` Check single string. `-z` empty string, `-n` not empty string.  
- `[[STR cond STR]]` Compare two strings. `==`, `<`, `>`, `!=`, `=~` (second string used as regex).  
- `&&`, `||`, `-a`, or `-o` for logical and and or.  

**Loops**  

`for variable in list; do ... done`  
`while [ condition ]; do ... done`  

**IO**  

`read variable_name`  

**Command Substitution**  

`result=$(command)` Stores commands output in result.  

	files_count=$(ls | wc -l)
	echo "There are $files_count files in the directory."

#### Example

Count arguments:  

	count=0  
	for arg in $*; do # also try with “$@”, “$*”  
	  count=$((count + 1))  
	  echo "Argument $count: $arg"  
	done  
	echo "Number of arguments: $#  
	
Read lines from file:  

	cat file.txt | while read line; do  
	  echo $line  
	done  

# Elisp

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

Hooks and Advice: Elisp supports hooks (functions run at certain points) and advice (modifying the behavior of existing functions). Hooks are defined with add-hook.  

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






# Networking

## The birth of the internet.  

### An Analog Version: Telephone Networks  

- Voice signals transmitted through analog electric signals.  
- **Circuit Switching**: Dedicated physical circuits established for each phone call. Remained until end of call.  
  - Guaranteed latency/throughput.  
  - Many points of failure, ie: a link or switch goes down.  
- **Electromechanical Switches**: Used relays for automatic call routing.  
  - physical devices that connected different wires to create a circuit.  
  - automatic call routing, reducing human intervention.  
- **Hierarchical Routing Structure**:   
  - Local exchanges connected phones within a local area.  
  - Tandem Exchanges: connected local exchanges.  
  - regional exchanges: connected tandem exchanges.  
  - long-distance Trunks: connected regional exchanges.  


### ARPANET: The First Internet @ Boelter 3420  

**Purpose**: Created by ARPA for resilient communication during the Cold War.  

- **Nodes**: Four initial nodes at UCLA, SRI, UCSB, and the University of Utah  
- ARPANET leased dedicated analog lines from telephone companies. Constant connection between points, unlike switched circuits used for regular phone calls.  
- **Modems**: ADC/DAC -> converts digital data from and into analog signals suitable for transmission over telephone lines. Converts back into digital data at the receiving end.  

1. **IMP (Interface Message Processors)**  
- **Function**: Acted as routers for the network.  
- **Responsibilities**:  
  - Receive messages from connected hosts.  
  - Store packets if necessary.  
  - Determine optimal routing paths.  
  - Forward packets to the next IMP on the path.  
- **Network**: Distributed mesh network, multiple paths between points. Resilient.  
2. **Host Computers**  
  - Each host is connected to the ARPANET through dedicated connections to their local IMP (Interface Message Processor).  
  - Heterogeneity: there is diverse range of host computers with different operating systems and hardware architectures. IMPs managed the complexities of interconnecting these diverse systems.  

3. **Packet Switching (by Paul Baran, RAND Corp, UCLA Alumni)**   
- **Message Breakdown**:  
  - Data is divided into small packets.  
  - Each packet includes:  
    - A header containing addressing information (source and destination).  
    - Sequence numbers to maintain order.  
    - Control data and byte sequences (header + payload).  
- **Independent Routing**:  
  - Packets are routed independently across the network.  
  - Each packet may take different paths depending on network conditions and available links.  
- **Reassembly at Destination**:  
  - The destination IMP reassembles the packets into the original message using their sequence numbers.  
- **Characteristics of Packets**:  
  - Best Effort Delivery: There is no guarantee that packets will arrive.  
  - Dropping: Packets can be dropped due to network congestion or errors.  
  - Out of Order Arrival: Packets may arrive in a different order than they were sent.  
  - Latency: There may be delays in packet delivery.  
  - Duplication: Packets can be duplicated, especially if a router is misconfigured.  
  - IMPs perform basic error detection on packets.  
 
#### ARPANET FLow:

1. A user on a host sends a message.  
2. The host breaks the message into packets.  
3. Packets are sent to the connected IMP, which:  
   - Receives packets (no guarantees on delivery).  
   - Examines the destination address.  
   - Consults the routing table.  
   - Forwards packets to the next IMP.  
4. The destination IMP reassembles packets and delivers the message to the destination host.  

## Modern Networking

### Internet Protocol Suite

Commonly known as the TCP/IP model. A combination of protocols, governing operation of the internet. Structured in layers that each serve a purpose.  

#### 1. **Link Layer (Network Access Layer)**  
- **Purpose**: Facilitates communication between adjacent nodes on the same local network.   
- **Function**: Handles physical transmission of data over network hardware.  
  - Physical Addressing: Uses MAC (Media Access Control) addresses to identify devices on the local network.  
  - Access Control: Determines how devices share the network medium (e.g., via CSMA/CD in Ethernet).  
  - Error Detection and Correction: Identifies and corrects errors in data transmission at the physical layer.  
- **Key Protocols**:  
  - Ethernet: The most common LAN technology, using a bus or star topology.  
  - Wi-Fi: Wireless networking standard, allowing devices to connect without physical cables.  
  - PPP (Point-to-Point Protocol): Used for direct connections between two nodes, often over serial links.  
- **Example**: A computer connecting to a router via Ethernet uses MAC addresses to identify itself on the local network.  

#### 2. **Internet Layer**  
- **Purpose**: Manages packet routing through the network, ensuring data is sent to the correct destination.  
- **Key Protocols**:  
  - **IPv4**: (Internet Protocol version 4) The most widely used version, providing an addressing scheme with 32-bit addresses (e.g., `192.168.1.1`).  
  - **IPv6**: (Internet Protocol version 6) Developed to address the limitations of IPv4, using 128-bit addresses (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).  
- **Packet Structure**:  
  - Version: Indicates the IP version.  
  - IHL: Internet Header Length, specifying the entire IP header's length.  
  - DSCP: Differentiated Services Code Point, indicating the type of service.  
  - ECN: Explicit Congestion Notification, info on the route (network) congestion.  
  - Total Length: Length of the entire packet (header + data).  
  - Flags: Control flags for fragmentation (e.g., "Don't Fragment").  
  - Fragment Offset: Indicates the position of the fragment in the original packet.  
  - Protocol: Tells the receiving internet layer what transport layer protocol this packet belongs to.  
  - Source Address: The IP address of the sender.  
  - Destination Address: The IP address of the intended recipient.  
  - Options: Optional fields for additional features.  
- **Example**: A web page request from a browser sends an IPv4 packet to the web server with the sender's and receiver's IP addresses.  

<img src="https://upload.wikimedia.org/wikipedia/commons/6/60/IPv4_Packet-en.svg" alt="IPv4 Diagram" style="display:block;margin-left:auto;margin-right:auto;width:60%;height:auto;">


#### **3. Transport Layer (Host to Host Layer)**  
- **Purpose**: Ensures complete data transfer between hosts, providing reliable or unreliable communication based on the protocol used.  
- **Functions**: Controls flow of data and reliable delivery.  
  - Segmentation and reassembly of data.  
  - Flow control.  
  - Error control (in TCP).  
  - Port addressing. Distinguish between applications on a host.  
- **Key Protocols**:  
  - **TCP (Transmission Control Protocol)**:  
	- Connection-Oriented: Establishes a connection before data transfer.  
	- Reliable: Guarantees data delivery through acknowledgments and retransmissions.  
	- Flow Control: Adjusts the rate of data transmission based on network congestion.  
	- **Example**: When downloading a file, TCP ensures all packets are received and assembled in the correct order, requesting retransmission of any lost packets.  
  - **UDP (User Datagram Protocol)**:  
	- Connectionless: Sends packets without establishing a connection.  
	- Unreliable: Does not guarantee delivery, order, or error correction.  
	- Thin layer over IP.  
	- **Example**: Streaming video uses UDP because timely delivery is more critical than perfect accuracy; lost packets are acceptable.  

#### 4. **Application Layer**
- **Purpose**: Interfaces directly with end-user applications, providing protocols for data exchange over the network. Assuming we can send reliable data, provides the interface for applications to access network services.  
- **Function**: Application-specific formatting and presentation. Session management. Interface with OS and applications.  
- **Key Protocols**:  
  - **HTTP (Hypertext Transfer Protocol)**: The foundation of data communication on the web.  
  - **FTP (File Transfer Protocol)**: Used for transferring files over the Internet, allowing users to upload and download files.  
  - **SMTP (Simple Mail Transfer Protocol)**: Protocol for sending emails.  
  - **DNS (Domain Name System)**: Translates domain names into IP addresses for identification.  
  - **DHCP (Dynamic Host Configuration Protocol)**: Assignes IP addresses and other paramters to devices on a network.  
- **Example**: A web browser uses HTTP to request web pages from a server, sending GET requests to retrieve resources and receiving HTML in response.
 
The Internet Protocol Suite is essential for ensuring that data is transmitted efficiently and accurately across the Internet, utilizing a layered approach to handle various aspects of networking. Each layer has specific protocols designed to address unique challenges in communication, enabling the seamless functioning of modern Internet services.  
 
### **HTTP (Hypertext Transfer Protocol)**  

An Application Layer Protocol!  

- **Requests**: Various types such as:  
  - GET: Requests data from a specified resource.  
  - POST: Sends data to server to create/update a resource (e.g., form submission).  
  - PUT: Updates an existing resource with new data.  
  - DELETE: Removes a specified resource.  
  - HEAD: Similar to GET but retrieves only headers.  
- **Responses**: Include status codes that indicate the outcome of the request  
	- Status: `200 OK`, `404 Not Found`, `301 Moved Permanently`, `500 Internal Server Error`.  
	- Headers: Information about response, content type, length, caching directives.  
	- Body (Optional): Contains requested data if any. (HTML, images, JSON)  
- **Versions**:  
  - **HTTP/1.0**: Single requests with no persistent connection. Inefficient because new TCP connection per request involves a lot of overhead.  
  - **HTTP/1.1**: Supports persistent connections and chunked transfer encoding, allowing multiple requests over a single connection.
	- Virtual Hosts: a single web server can host multiple domains on the same IP address. Differentiates requests based on domain name provided. Cost effective for server management.  
	- Pipelining: Clients can send multiple HTTP requests without waiting for corresponding response.  
		- Limitations in 1.1: Potential head-of-line blocking, where first request must be completed before processing subsequent requests.  
  - **HTTP/2**: Introduces multiplexing and header compression, improving performance.  
	- Multiplexing: multiple streams of data over a single connection simultaenously. Each stream is independent. Don't need to return in order.  
	- Elimanted head-of-line blocking issues for pipelining by allowing multiple requests/responses to be interleaved.  
  - **HTTP/3**: Built on QUIC, enhancing speed and reducing latency, especially for streaming.  
	- Good for streaming, better latency.  
	- More multiplexing built on UDP not TCP.  

### Browser Rendering

#### HTML  
The content retrieved via HTTP.  
- **Origins**: SGML (Standard Generalized Markup Language, IBM)  
  - Too complex: too flexible for the web and complexity slowed down browsers.  
- **Declarative**: HTML is a declarative language.  
  - Describes structure and presentation of text. (HTML, SGML, XML)  
	- 對方: Imperative. Gives instructions for a computer to perform.  
- **Elements**: Corresponds to a node in the tree that represents the document.  
  - Tags `<tag> ... </tag>`. Each element is written as a tag.  
	- A void element `<tag/>` cannot have any child nodes.  
	- A tag has attributes, treated as data stores in the treenode.  
	  - ie: `tag attr="val" attr2="val2"/>`.  
- **DTD**: (Document Type Definition)  
  - Used to define the structure and elements of HTML documents.  
  - Standardized way to validate HTML.  
  - maintained by W3C, and used in HTML 1-4.
	- When new elements were needed, DTD needed to undergo a formal organizational process.  
  - HTML 5: Moved away from strict DTDs, a more flexible and evolving standard.  
	- Faster innovation, more forgiving of errors, wider range of document structures.  

#### XML (eXtensible Markup Language)  
  - XML is a standard syntax for data representation. A branch of SGML developed by W3C and SGML.
- **Features**:  
  - Syntax: XML uses a syntax similar to HTML but does not include built-in elements. We define our own elements to suit our specific data structure.  
  - Primarily concerned with data storage and transport.  
  - Structure: Uses angle brackets for markup.  
  - Data Representation: Send hierarchical data (trees) over communication links.  
  - Primarily used for data storage and transport, not presentation.  

#### DOM Document Object Model  
  - The DOM is a spec that describes the tree data structure used to represent HTML and XML documents.  
- **Functionality**:  
  - Element Access: Provides methods for accessing element attributes and child elements.  
  - Navigation: Allows for navigation through the hierarchical tree structure of the document.  
  - APIs: Offers APIs for building, searching, and editing trees. JavaScript is the most popular language for interacting with the DOM.  
  
<img src="https://www.w3schools.com/js/pic_htmltree.gif" alt="IPv4 Diagram" style="display:block;margin-left:auto;margin-right:auto;width:60%;height:auto;">

#### CSS (Cascading Style Sheets)
- CSS is used to separate data from presentation, managing the style and visual aspects of web documents.  
- **Benefits**:
  - Consistency: Enables the application of styles consistently across multiple pages through external stylesheets.  
  - Flexibility: Provides control over every aspect of visual presentation, for richer UX.  
  - Responsiveness: Facilitates design of websites that adapt to different screen sizes and devices.  


#### Javascript
- JavaScript serves as a dynamic programming language. Allows for imperative coding within HTML documents.  
- **Features**:
  - Dynmic scripting: execute code directly in browser.  
  - DOM Manipulation: Can dynamically alter DOM trees, enabling interactive web applications.  
  - Asynchronous Programming: techniques such as AJAX allow fetching of data from servers without reloading entire page.  
- **JSON**: (JavaScript Object Notation) a lightweight alternative to XML, offering a smaller and easier-to-use data format. Used for data interchange. Easy to write and read.  
- **Limitations**: "Fails the CSS DOM hope"  
  - An ideal of using JavaScript to create complex layouts and styles that could be more efficiently handled by CSS. JavaScript's imperative nature can sometimes lead to less efficient and less maintainable code.  
  - Javascript execution can block rendering, performance bottlenecks.  

#### JSX (Javascript XML)  
- A syntax extension for JavaScript that allows you to write HTML-like code within JavaScript files.    
- Primarily used in React apps.  
- **Pros**:  
  - Readable: Easier to understand than nested JS functions calls when creating UI elements.  
  - Maintainable: Simplifies creation/management of UI structures.  
  - Type checking: catch errors earlier.  
- **Cons**:  
  - Learning curve for people new to JSX, how to integrate with JS.  
  - Build process: requires a build step to transform into normal JS.  
  - Debugging: Error messages could refer to compiled JS not original JSX.  
  - Verbose: For simple UI elements, more verbose than plain JS (or template literals)  
  - Tightly coupled with React.  
  
#### Browser Rendering Pipeline
- **Process Overview**: The rendering pipeline transforms HTML, CSS, and JavaScript into a visual display as follows:  

> **HTML + CSS + JavaScript** →  
> **DOM + CSSOM** (Parsing)→  
> **Render Tree** (Rendering)→  
> **Layout** →  
> **Paint** →  
> **Composite** →  
> **Visual Display**  

1. **Parsing**:  
   - HTML Parsing: Converts HTML into the **DOM** (Document Object Model).  
   - CSS Parsing: Converts CSS into the **CSSOM** (CSS Object Model) tree structure.  
   - JavaScript Compilation: JavaScript can modify the DOM and CSSOM, potentially requiring re-rendering to reflect changes.  
2. **Rendering**: Browser combines DOM and CSSOM to create the **Render Tree**. Represents the visual structure of page: contains only the visible elements.  
3. **Layout**: Browser calculates the size and position of each element in the Render Tree, determining the geometric layout of the content.  
4. **Paint**: Browser draws pixels for each element on the screen, including:  
   - Filling colors  
   - Applying background images  
   - Drawing borders  
   - Rendering text  
6. **Composite**: Elements in the page may be layered; the browser composites these layers to create the final visual representation.  
   - Compositing can enhance performance, especially during animations and transitions, as changes to a single layer do not necessitate repainting the entire page.  
7. **Incremental Rendering**:  
   - The browser can begin rendering an element as soon as it encounters the opening tag, allowing for a quicker but incomplete display of the webpage.  
   - ie: ` <story headline="Big Long Demo"> 3GiBs </story>`  
     - The browser guesses the layout and decides to ignore off-screen elements initially.  
     - Attributes with low priority are executed last.  
     - Rendering of tables may trigger a "refresh" of the screen, leading to JavaScript execution multiple times.  
  
### Code Examples

#### HTML and CSS:  

	<!DOCTYPE html>
	<html>
	  <head>
		<title>My Styled Page</title>
		<link rel="stylesheet" href="style.css">
	  </head>
	  <body>
		<h1>This is a heading</h1>
		<p>This is a paragraph.</p>
	  </body>
	</html>
	
	/* style.css */
	h1 {
	  color: navy;
	  font-size: 32px;
	}
	p {
	  color: gray;
	  line-height: 1.5;
	}


## Application Styles

#### Standalone Applications

A standalone app (also known as desktop app or thick client) runs on a single computer, doesn't need a network connection for its functionality. Processing, data storage, and resources on host device. (ie: Word, Photoshop, a calculator app).  

- Pros:  
  - performance is fast, responsive, don't rely on network speeds.  
  - work without internet connection.  
  - data is private to machine.  
- Cons:  
  - Little collaboration - sharing data is manual.  
  - Potential version inconsistencies since each user installs updates independently.  
  - Resource intensive: CPU, memory, storage.  
  
#### Client Server Applications

Two programs, a client and a server. Client presents information to the user, requesting data and services from the server. The server handles data processing and storage. (ie: email, social media, banking).  

- Pros:  
  - Data is centralized. Accessible from any client.  
  - Multiple clients can access and modify data, collaborative.  
  - Updates are easy: server admin just needs to update software.  
- Cons:  
  - Depends on network, needs stable internet.  
  - If server is overloaded, performance might suffer.  
  - Centralized data means a single point of failure for security breaches.  
  
#### Peer-to-Peer Applications

Each computer acts as client and server. Resources are shared mutually without a central server. Connect to multiple servers. (ie: BitTorrent).  

- Pros:  
  - Decentralized, no single point of failure. Operational even if peers disconnect.  
  - Scalable. More people means more capacity.  
  - Efficient distribution. Ie: large files downloadable faster by pulling from multiple sources.   
- Cons:  
  - Security risk: vulnerable to malware.  
  - Performance may fluctuate depending on number of peers and connection speeds.  
  - Difficult to manage and monitor the network, without central control.  


//Still need to include: emacs. processes and users


## Midterm Tips:  

Content: 
- Topics: emacs, emacs lisp, shell scripting, python scripting, regex, networking. (no react)  
- Questions on... Bash scripting. Python scripting (writing function, writing script). Regex. Reading/Fixing Emacs Lisp. Comparison questions: pros and cons.


Writing Notes: directory entry = file

NO MCQ!  

Tips: 
- Print out assignments!  
- Check LA Megathread on Piazza. Print out worksheets.  
- Practice Python, Bash, Emacs, Lisp.  
- Don't worry about syntax. Learn important libraries (command line (argparse), random).  
- There might be impossible questions. Might ask to explain bugs.  
- pay attention to wording.  
- creative questions: might allow both yes or no, with reasoning.  

### Files, Editing, Shell

  - PATH searches through each directory in order left to right.  
    - PATH=$PATH:/usr/local/cs/bin <- adds this cs bin to the end of the path, so it will be the last to run if there exists other copies in previous directories in the path.  
	- instead run PATH=/usr/local/cs/bin:$PATH.  
	- PATH=/usr/local/cs/bin:.:/usr/bin
	  - security risk: the dot represents current directory, so current directory will lie in the path. 
	  

### Commands and Basic Scripting:
- unix shell for scripting.  
- pattern matching: wildcards and ere.  
- commands: grep, find, awk, sed.  
- pipelines and redirection.  
- regex!  


Regex:  
- review what extended mode does for grep.  
- * means zero or more of any character, but within a character class [] just matches the literal character.  
- ^ means start of line, except when its in a character class [] in which case it means 'not'.  
- other special characters: `.` `^` `$` `*` `+` `?` `[]` `|`.  


Shell:  
- A | B -> both are run at the same time, A's stdout is connected to B's stdin.  
- A & B -> A is started in the background. B is started immediately. A and B are ran in parallel.  
- A && B -> runs A first, then runs B. Only when A succeeds, if A exits with a status of 0. This means it does not run A and B in parallel.  

Emacs:  
- implementation of emacs.  

Principles of software construction:  

### Python  

Python:  
- Dictionaries  
- circular reference  
- keys must be hashable,  
- Mutable vs Immutable types.  
- Garbage Collector  
- functions vs scripting (if it says write a program its a script!).  
- type conversion.  
- how slicing works.  
- print in python automatically does a newline.  
- sys.stdin -> take from std input. input() does something else?  

### Networking

Networking:  
- version control  
- Order of network protocols.  
  - User/Application (Firefox) -> Application (HTTP) -> Transport (TCP) -> Network (IP) -> Link (Ethernet driver) -> Hardware (Ethernet)  
  - Opposite order depending on recipient/sender.  
  - Https vs circuit switching??  
- out of order execution. -> when working with networking, its harder to keep state in sync.  
- same with stale caches.  
- HTTP -> 1 vs 2 vs 3. Support for streaming data/speed.
  - new protocols? 

Browser Caching:  
- Different browser vs. different device vs. clearing cache.  
- state caching  
- multiple places of caching, isp, local cache, web server.  
- different user agents.  
- stale caching.  

Bash Scripting:  
- `tr`, `grep`, `sort`, `comm`, `<&0`.  

Character encoding!
- ASCII, UTF, other things.  
