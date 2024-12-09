# C  

Core Language Philosophy:  
- Procedural -> focused on functions and data separately, not object-oriented.  
- Simplicity -> close to hardware, with fewer abstractions.  
- Manual Memory Management -> no automatic cleanup mechanisms.  

### Differences with C++

- No classes or objects. Can't encapsulate data and methods. No inheritance or polymorphism.  
- No function overloading. Each function needs a unique name.  
- No references. Parameter passing always involves values or pointers.  
- No templates. Generic programming must use void pointers or macros. Type safety is managed manually.  
- No STL (no built-in containers... vectors, lists, maps).  
- No exception handling: error handling typically uses return values. Must check function returns explicitly.  
- No bool type for C89: use integers.  


`main` function: the entrance to our program, returns a value of type int.  

We use libraries for basic functions: `stdio.h` for `printf`.  

## Syntax  

### I/O

**Format specifiers**

`%d` Integer  
`%.2f` Float with 2 decimals  
`%s` String  
`%c` Character  
`%p` Pointer  

    int num;
	char str[100];
	float fnum;

	scanf("%d", &num);     // Read integer
	scanf("%s", str);      // Read string (no & needed for arrays)
	scanf("%f", &fnum);    // Read float
	scanf("%[^\n]s", str); // Read entire line including spaces
	fgets(str, sizeof(str), stdin); // Safer string input
	
#### Strings

`sizeof(str)` Total allocated memory for the string.  
`strlen(str)` Get length.  

`strcpy(dest, src)` Copy.  
`strncpy(dest, src, sizeof(dest) - 1)` Safely copy, supplying a max size.  

`strcat(dest, str)` Concatenate to end of dest.  
`strncat(dest, str, sizeof(dest) - strlen(dest) - 1)` Safely concatenate.  

`strcmp(str1, str2)` Compare two strings.  

`atoi("123")` String to int.  
`atof("3.14")` String to float.  
`strtol("123", NULL, 10)` String to long with base.  

	// Parsing strings
	char* token = strtok(str, " ,");
	while token != NULL) {
		printf("%s\n", token);
		token = strtok(NULL, " ,");
	}

#### Structs
 
- Flexible array members must be last member.  
- pointer members require manual memory management.  

	// Structure with pointer members
	struct DynamicPerson {
		char* name; // Requires manual memory management
		int age;
		char** hobbies; // Array of strings
		int hobby_count;
	};
	
	// Function to initialize DynamicPerson
	struct DynamicPerson* createPerson(const char* name, int age) {
		struct DynamicPerson* person = malloc(sizeof(struct DynamicPerson));
		if (!person) return NULL;
		person->name = malloc(strlen(name) + 1);
		if (!person->name) {
			free(person);
			return NULL;
		}
		strcpy(person->name, name);
		person->age = age;
		person->hobbies = NULL;
		person->hobby_count = 0;
		return person;
	}
	
#### Function Pointers and Callbacks

Functions that are passed as an argument to other functions. A function pointer is a variable that stores the address of a function, allowing you to call the function indirectly through the pointer.  

	typedef int (*Operation)(int, int); 
	int apply(Operation op, int a, int b) {
		return op(a, b);
	}
	
	// Creates a type alias named Operation for a function pointer, taking two ints and returning an int.  
	// apply is a function that takes an Operation, a pointer to a function that takes two ints and returns an int.
	

#### Error Handling

In C, error handling is done through return values.  

	// Error/Exit codes
	enum ErrorCode {
		SUCCESS = 0,
		ERROR_MEMORY = -1,
		ERROR_INVALID_INPUT = -2,
		ERROR_FILE_NOT_FOUND = -3
	};
	
	// Function with error code
	int processData(const char* filename, int* result) {
		if (!filename || !result) return ERROR_INVALID_INPUT;
		// ... process data ...
		return SUCCESS;
	}
	
	// errno usage
	#include <errno.h>
	if (errno == ENOMEM) {
		// Handle out of memory
	}


### Memory Management

#### Memory Structure  

Memory is organized into regions that serve different purposes and have different *growth directions*. 

![memory-layout-c](https://images.javatpoint.com/cpages/images/memory-layout-in-c.png)


Memory is split into blocks.  
- each allocated blocks has metadata to track its size and status.  
- metadata stored in a header structure before the actual data.  
  - size_t size;  
  - int is_free;  
  - struct block_meta* next;  
  
Blocks are arranged as follows:  
- metadata block -> allocated memory -> next metadata block.  

Splitting blocks: if a free block is larger than request size, remainder can be kept as a smaller free block.  
- Coalescing adjacent free blocks: when multiple blocks are freed, allocator can merge them.  
- Fragmentation: heap becomes fragmented as many allocations/deallocations occur.  

Block selection: different algorithms can be used to choose which free block to allocate.  
- each one has different performance characteristics and fragmentation patterns.  
- First fit: searh for first block >= requested size. Quick but more fragmentation.  
- Best fit: Search for smallest block >= requested size. Slower but less fragmentation.  
- Worst fit: Search for largest block: good for splitting, poor memory utilization.  

 

#### Malloc Heap Management  

- If a free block exists in the heap that's large enough to satisfy the malloc request.  
- If no suitable block is available, the heap may be expanded by requesting memory from OS.  

	void* malloc(size_t size); // raw memory allocation  
	void* calloc(size_t num, size_t size) // Allocated zeroed  
	void* realloc(void* ptr, size_t size); // Resize allocation  
	void free(void* ptr); // Free memory  
	
	// Common allocation patterns
	
	int* intp = (int*)malloc(sizeof(int)); // cast void* to int*
	if (intp == NULL) return 1; // always check for success
	
	int* arrayp = (int*)malloc(n * sizeof(int));
	if (arrayp == NULL) return 1;
	
	struct Person* p = struct(Person*)malloc(sizeof(struct Person));
	if (p == NULL) return 1;
	
	int** matrix = (int**)malloc(rows * sizeof(int*));
	for (int i = 0; i < row; i++) {
		matrix[i] = (int*)malloc(cols * sizeof(int));
		if (matrix[i] == NULL) {
			// Handle error
			for (int j = 0; j < i; j++) {
				free(matrix[j]);
			}
			free(matrix);
			return 1;
		}
	}
		
	

#### System Call Interface  

- `malloc()` interacts with OS through system calls.  
- `sbrk()` and `brk()` are traditional UNIX system calls for managing program break.  
- modern systems use `mmap()` for large memory allocations.  

	void* sbrk(intptr_t increment); // increments sizeo f program break by increment.  
	int brk(void* addr); // set program break to the specified location.  
	
	void* simple_malloc(size_t size) {
		static void* heap_end = NULL;
		if (heap_end == NULL) {
			heap_end = sbrk(0); // Get current break
		}
		void* block = sbrk(size);
		if (block == (void*)-1) {
			return NULL; // Out of memory
		}
		return block;
	}
	
