## Functions

```c
return-type function-name (parameters) {
	// body
}
```

- If a function will be accessed before it is defined, it can be **prototyped**:
	- `return-type function-name (parameter types);`

### Pass by value/Pass by Reference

- Arguments to functions are **passed by value**.
- To allow a function to modify arguments, we need to **pass by reference**:

```c

void swap(int *a, int *b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}
```

### Function pointers

- Declaring a function pointer:
```c
long (*ptr)(int);
ptr = &square;
```
- The above pointer `ptr` points to a function that **takes** an `int`, and **returns** a **long**.
- `ptr` is then set to point to the address of `square`.

- We can then use `ptr(<params>)` to return the value of `square(<params>)`.

## Types

### Basic types

|Identifier|Range|
|----------|-----|
|`int`|$[-32768,32767]$|
|`float`|$[-1.2*10^{-38},3.4*10^{38}]$|
|`double`|$[-2.2*10^{-308},1.8*10^{308}]$|
|`char`|ASCII|

### Specifiers

|Specifier|Range|
|---------|-----|
|`short int`|$[-32768,32767]$|
|`unsigned short int`|$[0,65535]$|
|`unsigned int`|$[0,4,294,967,295]$|
|`long int`|$[-2147483648,2147483647]$|

### Conversion

- Types are coerced if possible. e.g. assigning an `int` to `float` type will 'promote' it to a `float.

### Constants

1. `int const MAX = 10;`
2. `#define MAX 10`

### Composite types

#### Arrays

- Elements of an array are assigned consecutive memory addresses. 

##### Array iteration using pointers

```c
int arr[5];
int *ptr;

ptr = &arr[0]; // *ptr points to arr[0].
*(ptr+1) // points to arr[1].
```

Warning: `*(ptr+1)` = arr[1], but `*(ptr)+1` = `arr[0]+1`.

#### Pointers

- A **pointer** is a type referencing another value, by storing its address.
- Declared by `int *ptr`.

- Special operators:

|Operator|Action|
|--------|-----|
|`*`|"Dereference". Given a pointer, obtain the value of the object referenced.|
|`&`|"Address-of". Given an object, use & to point to it. The `&` operator returns the address of the object pointed to.|

```c
int a = 42;
int *p; // initialize a pointer to int
p = &a; // point p to the address of a.

// accessing *p will return 42.
```
- This allows for aliasing and accessing/modifying the same memory location from different names.

##### Constant pointers

- `int * const ptr1 = &a`
- The **address pointed to** cannot change:
	- i.e. `ptr1 = &c; // Error: Assignment to const identifier`

##### Pointers to constants

- `int const * ptr2 = &b`
- The value of the object pointed to **cannot change**. It can, however, be pointed elsewhere.
	- i.e. `*ptr2 = 7; // Error: Assignment to const location` 

##### Constant pointer to constant 
- `int const * const ptr3 = &b;`
- We can change **neither the address** the pointer holds, **nor the value** of the object it is pointed at.

#### `Struct`

##### Declaration and instantiation

- Form 1

```c
struct st {
	int a;
	long b;
	char c;
};

struct st x; 
``` 

- Form 2

```c
typedef struct {
	int a;
	long b;
	char c;
} st;

st x;
```

Attention: a `struct` always needs to be terminated with a `;`.

##### Initializing members at declaration

- Form 1

```c
st x = {1,2,3};
```

- Form 2

```c
st c = { .a = 1, .b = 2, .c = 3};
```

##### Assigning values after declaration

- Form 1

```c
x.a = 1;
x.b = 2;
x.c = 3;
```

- Form 2

```c
st y;
y = x; // Copies the member values of x to y
``` 

##### `struct` member access with pointers

- Form 1

```c
st *ptr = &x;
(*ptr).a = 1;
```

- Form 2

```c
ptr->a = 3;
```

#### Unions

- Data type that allows you to store different data types in the same memory location.
- Only one member can contain a value at any given time. 
- The memory used by the union will be large enough to hold the largest member.

```c

union Data {
	int i;
	float f;
	char str[20]
}
```
	

## Variables

### Scope

- **Global variables** are defined at the top of the program, and can be accessed by any function.
	- Have default initializations.
- **Local variables** are accessible only within the block that defines them.
	- Do **not** have default initializations

- If a local variable has the same name as a global one, the local variable takes precedence, known as *shadowing*.

### Modifiers

- `static`: the variable/function is visible only from within the file it is defined in.
- `extern`: the variable/function is defined outside the current file. 
- Default : indicates that the variable/function is defined within the current file, and it is visible in other files. 

## Managing memory

- The `malloc()` function returns a pointer to a block of memory on success.
	- If it fails, it returns NULL.

- Requesting memory for an array of 3 integers:
	- `int *array = malloc(3 * sizeof(int));`

- Important to check for failure:
	- `if (array == NULL)`

- Once we're done:
	- `free(array)`;

## ADTs/Data structures

### Linked list

```c
typedef struct {
	int data;
	struct node *next;
} node;

node *head;
head = malloc(sizeof(node));
head->data = 5;
```
