# GCC and Makefiles

## GCC

Gnu Compiler Collection: Supports multiple languages, used widely for Unix/Linux.  

**`gcc -o OUTPUT SOURCES`**


- `-E` complete only preprocessing.  
- `-S` compile to assembly.  
- `-c` compile to an object file without linking.  

- `-I<DIR>` specify an include directory.  
- `-L<DIR>` specify the library linking path.  
- `-l<NAME>` link the library NAME.

Debugging:

- `-Wall` enable all common warnings.  
- `-Wextra` unused function paramters, missing field initializers, sign comparison issues.  
- `-Werror` Treat all warnings as errors.  

- `-O` optimize level. 0, 1, 2, 3.  
- `-Os` optimize for size over performance.  
- `-Og` optimize for debugging experience

- `-g` Enable debugging information you can  see in GDB: 1, 2, 3.

Other: 

- `-n` Dry run mode: print commands without running.  
- `-t` Update modification times of targets as if running commands without actually running it.  
- `-q` Check if targets are up to date without building.  
- `-f` specify a makefile name.  
- `-j` specify number of commands to run simultaneously.  
- `-C` change to specified directory before reading makefiles.  
- `-B` force rebuilding of all targets, even when up to date.  
- `-k` continue building other targets even when errors occur.  

## Makefiles

target: dependencies
	commands
	...
	
`*` wildcard.  
`%` match any string.  
`@` suppress comments.  
`-` add dash before a command to make it keep going even if the command fails.  
`$(VAR_NAME)` reference a variable.  
`foo = abc` to assign a value, or `foo := abc` to evaluate value at time of assignment.  

`$@` target name.  
`$<` first dependency.  
`$^` all dependencies.  
`$*` Stem

`.PHONY: RULES` Use phone to declare a phony target, one that has no output files.  


## Other GCC Options

### Optimization Related Options

#### Function Optimizations
■ -ffunction-sections # Place each function in its own section
■ -fdata-sections # Place each data item in its own section
■ -finline-functions # Integrate simple functions into their callers
■ -fno-inline # Don't integrate functions into their callers
■ -fomit-frame-pointer # Don't keep frame pointer in register
■ -foptimize-sibling-calls # Optimize sibling and tail recursive calls
#### Loop Optimizations
■ -funroll-loops # Unroll loops whose number of iterations can be
determined
■ -funroll-all-loops # Unroll all loops
■ -floop-optimize # Perform loop optimizations
■ -ftree-loop-vectorize # Vectorize loops
■ -floop-block # Block loops to improve cache performance
#### Code Size Optimizations
■ -ffunction-sections # Place each function in its own section
■ -fdata-sections # Place each data item in its own section
■ -fmerge-constants # Attempt to merge identical constants
■ -fmerge-all-constants # Attempt to merge all constants
■ -fno-common # Do not put uninitialized globals in common block

■ -march=native enable hardware intrinsics that perform better than their software counterparts. 

### Debugging and Diagnostics
#### Debug Information
■ -feliminate-unused-debug-types # Remove unused types from debug
info
■ -fno-eliminate-unused-debug-types # Keep all types in debug info
■ -fdebug-prefix-map=OLD=NEW # Remap debug info file paths
■ -fvar-tracking # Better debug info for optimized code
#### Runtime Checks, we talked
■ -fstack-protector # Enable stack protector
■ -fstack-protector-all # Enable stack protector for all functions
■ -fsanitize=address # Enable AddressSanitizer
■ -fsanitize=thread # Enable ThreadSanitizer
■ -fsanitize=undefined # Enable UndefinedBehaviorSanitizer
### Code Generation Options
#### Exception Handling
■ -fexceptions # Enable exception handling
■ -fnon-call-exceptions # Enable exceptions for non-call instructions
■ -fno-exceptions # Disable exception handling
■ -funwind-tables # Generate unwind tables for stack unwinding
#### Runtime Type Information
■ -frtti # Generate run-time type descriptor information
■ -fno-rtti # Disable run-time type descriptor information
#### Position Independent Code
■ a body of machine code that executes properly regardless of its
memory address.
■ -fpic # Generate position-independent code (small model)
■ -fPIC # Generate position-independent code (large model)
■ -fpie # Generate position-independent executable
■ -fPIE # Generate position-independent executable (large
model)

### Language Feature Control
#### C++ Features
■ -fno-enforce-eh-specs # Don't enforce exception specifications
■ -fstrong-eval-order # Enforce evaluation order of operands
■ -fno-threadsafe-statics # Don't generate thread-safe code for static
locals
■ -fvisibility-inlines-hidden # Hide inline function symbols
#### C Features
■ -fno-builtin # Not replace library functions with builtin compiled
code
■ -fno-asm # Don't recognize asm keyword

### Compatibility Options
■ -fno-strict-overflow # Don't assume signed overflow wraps
■ -fwrapv # Assume signed arithmetic wraps
■ -fno-trapping-math # Assume FP operations don't trap

### Common Option Combinations
 
Debug Build
■ CFLAGS="-fno-omit-frame-pointer -fstack-protector-all
-fsanitize=address -fvar-tracking -fno-inline"

Release Build
■ CFLAGS="-fomit-frame-pointer -ffunction-sections -fdata-sections
-fno-exceptions -fno-rtti -fvisibility=hidd



