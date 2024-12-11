# Low Level

## User/Kernel Mode

Desribes access to the system. Users are not given direct access to hardware. Kernel has complete access to hardware--can acccess any memory, issue any command.  

**System calls:** The way Users access kernel-level instructions.
- Ie: read, write, getpid, open, close are system calls.  
- Often system calls are used for I/O or disk operations...  
- Context switching (user <-> kernel) is expensive, we try to keep them to a minimum.  


> A user makes a sys call -> interrupt + swap to kernel -> kernel executes function -> flow returns to user mode with the output of the sys call.  

**Library calls** are higher level functions, the ones we interact with directly.  
- They function by making system calls, which are the only way to access kernel priviledges.  
- Ie: putchar, printf, etc...  

## Compilation

Turning a source file into a binary executable. We use a compiler such as gcc.  

`gcc -o prog prog.c` Compiles 

### Compilation Process

> Source Code -> Precompile -> Assembly -> Machine Code -> Executable Binary  

1. Preprocessing: Remove headers, macros, #define, comments from source code  

> #include <stdio.h>
> #define CONSTANT 5
> #ifdef ...
> // Some comment 

2. Compiler: Translate code to assembly language.  

3. Assembler: Assembly code to object file (machine code).  

4. Linker: Link imported libraries into code. This produces the final executable.  

**Static Linking**: directly copies library into the executable, at compile-time.  
- executable is self contained.  
- bulkier file, not flexible.  

**Dynamic Linking**: linked code is loaded at run-time.  
- requires `.dll` (dynamically linked library) or `.so` (shared object) files.  
- modular, but need to keep library files on the system.  


## Debugging

Debugging tools help us step through code, traceback calls, find values of parameters passed, manage memory.  

**Valgrind**: A tracing framework.  
- `gcc -g FILE.c -o FILE.exe` The -g flag tells gcc to include extra debugging information.
- `valgrind --leak-check=full ./file.exe` Show all information about memory leaks.  

**GDB**: Step through code line by line.  
- Check variable values, run commands, use breakpoints, traceback.  

`gdb a.out`
- `run [args]` or `run < file` Run the file with arguments.  
- `break [file]:LINE_NUM` Set breakpoint at line num, or by function name.  
- `info b` List breakpoints.  
- `delete/disable/enable NUM` Delete or disable a breakpoint by its breakpoint num.  
- `step [n]` Go to next n lines.  
- `next [n]` Go to next n lines, without going into functions.  
- `continue` Goes until next breakpoint.  
- `print var/exp` Print a variable or expression.  
- `watch var` or `rwatch var` Pauses when a variable is changed, or when a variable is read.  
- `list` List nearby lines.  
- `info` List info about a particular thing.  

- `attach pid` attach gdb to current running process, to debug something in production or running.  
- `backtrace` Show all the frames in the stack, one frame per line.  
- `watch` create a watchpoint: stops if object under watch changes.  
- `catch` create a catchpoint: stops for certain program events, (throws, exceptions, syscalls, etc...)  

- can debug a program on a target machine from a host machine: run program on target machine as `gdbserver :PORT_NUM ./buggy_program` and target it from host gdb with `target remote targethost:PORT_NUM`  


