# Programming in C

## Organizing C projects

### Kinds of files

- `.c` are source files.
- `.h` are header files, which contain function declarations.




### including headers

`#ifndef EXAMPLE_H_`
`#define EXAMPLE_H_`
`#endif`

### Structure of a C program
- every program starts with the header files that you __include__, e.g.
	- `#include "stdio.h"`
- Then, constants are initialized.
	- `#define TRUE 1`
	- `#define FALSE 0`
- Comments are added thusly:
	- `/* This is a comment */` for multiple lines
	- `// this is a comment` for single lines
- Functions are declared:
	- `func_name(int par1, int par2){_block_}`
	- *n.b. functions can also be declared here and defined later, often at the beginning of a program or in a separate header file*
- Then the __main__ function is declared, with a return type *int*
	- `int main () { __block __ }` 	

## Constants

###Integers
- Adding L or l at the *end* of a integer constant forces it to be a `long`.
	- `#define CONSTANT 1048536L` 
- Adding U or u at the *end* of a integer constant forces it to be `unsigned`.
- Adding `0X` or `0x` at the *beginning* of a integer constant forces it to be __hexadecimal__.
- Adding `0` at the *beginning* of a integer constant forces it to be __octal__.

###Real numbers
- Real number constants are type `double` unless otherwise specified. 
- Adding `F` or `f` at the *end* of a real constant forces it to be a `float`.
- Real number constants can be represented with scientific notation using E or e, suffixed with the sign of the exponent.
	- `#define REAL_CONSTANT 2.0e+5`
	- `#define ANOTHER_REAL_CONSTANT 3.0E-5` 

## Operators
	
### Arithmetic

- `+ - * / % ++ --` are all fairly self explanatory
- `/` for integer division, `%` for modulus

### Increment and Decrement

- `x++`, `x--` increment and decrement. In expressions, the __old__ value will be used.
- `++x`, `--x` increment and decrement as well -- but in expressions, the __new__ value will be used. 

- However, very important to correctly place the `++` or `--`
	- `++x` increments the variable and then uses the value
	- `x++` uses the value and _then_ increments the variable

### Bitwise

Operator|Effect|Conversions
-------:|-----:|-----------
`%`|bitwise AND| usual arithmetic conversions
`__pipe__`|bitwise OR| usual arithmetic conversions
`^`|bitwise XOR| usual arithmetic conversions
`<<`|left shift|integral promotions
`>>`|right shift|integral promotions
`~`|one's complement|integral promotions

-- `>>` is equivalent to dividing by 2
-- `<<` is equivalent to multiplying by 2

### Relational

Group 1|Group 2|Group 3
-------|-------|-------
`!` not| `>` bigger than| `&&` logical and
`==` is equal| `<` smaller than| `||` logical or
`!=` inequality| `>=` bigger than or equal to|  
.|`<=` smaller than or equal to

### Complex Statements and Assignment 
- relational operators can be assigned to variables.
- example:
````
int k = 1;
int flag = (k < 10); // flag is 0 until k < 10 evaluates as true
````


## Data Types
- Data type sizes/potential overflows can be avoided with the __sizeof__(*type*) call, or by reviewing __limits.h__
- __Casts__ can be used to force a type of an expression. Casts are defined by putting the type to be forced in parens, such as `(int)` or even pointers to types, like `(int *)`

### Integers & Chars

Type|format string|base
---:|-------------:|----
char|%c|n/a
unsigned short int|%u|decimal
unsigned int|%u|decimal
unsigned long int|%lu|decimal
signed short int|%d|decimal
signed int|%d|decimal
signed long int|%ld|decimal
int, short, char|%x|hexadecimal
int, short, char|%o|octal 

### Escape characters
Sequences|Represents
--------:|-----------
`\a`|audible alarm
`\b`|backspace
`\f`|form feed
`\n`|newline
`\r`|carriage return
`\t`|tab
`\v`|vertical tab
`\\`|backslash
`\'`|quote
`\"`|double quote
`\?`|question mark

### Arrays

- Arrays can be declared with the *type* of its members, and the number of indices in square brackets
- `double ar[100]` declares an array of `double`s indexed from `[0]`-`[99]`

- arrays can be multidimensional.
- `int three_dee[2][3]` declares an array `three_dee` with two members. each of those two members contains three `int`s.


#### initializing arrays with explicit size

`int classrooms[5] = {15, 18, 10, 23, 15};`

#### initializing arrays _without_ explicit size

`float heights[] = {3.0, 4.2, 5.6};`

#### easy printing array

```

void printArray(char dataName[], int dataSet[], int dataLength){
	for(int i=0; i<<ARRAY_MAX>; i++){
		print("%s[%d]: %d\n", dataName, i, dataSet[i]);
		
```

#### two dimensional arrays

```
int table[2][3] = {
	{132, 142, 23},
	{0, 76, 872}
}
printf("Row 1 Column 2 contains %d\n", table[1][2]
```

#### easy printing two dimensional array

``` 
void printTable(int table[<NUM_COLS>]){
	for(int i=0; i<<NUM_ROWS>; i++){
		for(int j=0; j<<NUM_COLS>; j++){
			printf("%4d",table[i][j]);
		}
		printf("\n");
	}
}
```


### Pointers

- Pointers are many things, but a useful application of them is to circumvent the pass by value mechanism and modify values directly in the global domain. 
- Pointers are also useful to 'walk' along an array. Incrementing a pointer to an array element will make it point to the next array element. 
- Pointers need to be declared like other variables. 
- the type prefacing the pointer indicates the type of variable it will point to, e.g. `int *ip` is of type `pointer to int`.
	- note here that the pointer has been declared, but until it is made to *point* to anything, it is *uninitialized*.

#### Initializing a pointer
```
int ar[5], *ip;
ip = &ar[3];
```
- The above snippet initializes the pointer to point to the third index of the array `ar`.
- the `&` operator indicates the *address of* a variable.
	- Applying the `&` operator to an operand returns a pointer to the operand. e.g

```
int i, j;
float f;
j = *i; 
```
- `&i` now is of type **pointer to int**
- `&f` now is of type **pointer to float**
	- if __j__ is a *pointer to int*, *__j__ is what the pointer points __to__.

#### Example of usage (circumventing pass by value)
```
#include <stdio.h>
#include <stdlib.h>
void
date(int *, int *);     /* declare the function */

main(){
      int month, day;
      date (&day, &month);
      printf("day is %d, month is %d\n", day, month);
      exit(EXIT_SUCCESS);
}

void
date(int *day_p, int *month_p){
      int day_ret, month_ret;
      /*
       * At this point, calculate the day and month
       * values in day_ret and month_ret respectively.
       */
      *day_p = day_ret;
      *month_p = month_ret;
}
```
- Note that it doesn't matter that the function returns *void* -- the values are passed back via the pointers, not the return statement. 

#### Incrementing pointers

expression|action
---------:|------
++(\*p)|pre-increment thing pointed to
(\*p)++|post-increment thing pointed to
\*(p++)|access via pointer, post-increment pointer
\*(++p)|access via pointer which has already been incremented

#### Untyped pointers

- Pointers can be converted using casts.
- `p = (float *)expression;`

#### Pointer operators

De-referencing is the process of telling the computer to go to the memory address you have here, and to manipulate the memory itself. To do that in C, you use the “follow-address operator”, `*`. So, when you have a memory address in a pointer variable `m`, `*m += 1` essentially tells the computer to first “walk over to that address”, and to then add 1 to whatever it finds there.

And finally, the `&`-operator, also known as “address-of”. The address-of-operator simply tells the computer to give you the memory address at which a particular variable is located. You can then stuff this address in a pointer variable and perform pointer arithmetics on it, or whatever you want.

#### Function pointers

The declaration of a variable holding a pointer to a function:

```
int doSomething(int first, int second)
{
	return first + second;
}

int		(*pointerToFunction)(int first, int second);
pointerToFunction = doSomething; 
```

- the variable declaration is in brackets to indicate that it is a function pointer. 


### Strings

- `include <string.h>`
- Strings in C are arrays of `char`, and null terminated.
	- Actually, a 'string' is of type `pointer to char`, because it points to the first element of 'hidden' array of type `char`.

- Walking along a char array using a pointer is an easy way to print a string of arbitrary length.

```
cp = "a string\n";
while(*cp != 0) { 		// *cp points to the value of the first element of the array
printf("%c", *cp);
cp++; 			// increment where cp points to
```

### User defined types

#### `Struct`

```
struct studentDBEntry
{
	char firstName[20];
	char lastName[20];
	int age;
	bool isGraduating;
};

struct studentDBEntry englishClass[20];
englishClass[0].age = 16;

// the above creates an array of 20 studentDBEntry structs and assigns age 16 to the first element
```

#### `enum`

- Formally known as _enumerated symbolic constants_
- Often used to declare constants and avoid magic numbers.
	- *Limitation*: `enum` constants are limited in type to `int` or `char`.

```
enum choices
{
	YES = 1,
	NO = 2, 
	MAYBE = 3,
};
```
- Warning: Like `struct`, an `enum` needs a terminating semicolon. 

#### Constants via preprocessor

- The `#define` keyword can be used to define constants of any kind, including `float` and string literals. 

```
#define PI = 3.14159
#define GRAMS_PER_POUND = 454
#define DEFAULT_VOLUME = "Macintosh HD"
```
Warning: These are _not_ terminated with a semicolon, because the preprocessor treats them specially.

#### `Typedef`

- Say you want a type for huge integer numbers. 

```
typedef long long int	bigNum;
bigNum myNumber = 140975172;
```

- This is also handy to have types that are implicitly defined as pointers:

`typedef int* pointerToInt;`

It can equally be used to make types of `struct` and `enum`.

###Bitfields

```
#define FLAG_ONE	(1 << 0) // 0001
#define FLAG_TWO	(1 << 1) // 0010
#define FLAG_THREE	(1 << 2) // 0100
#define FLAG_FOUR (1 << 3) // 1000
```
- We're bit shifting 1 to the left here, because 1 is the rightmost bit activated and all others 0. So in a 4 bit variable, shifting `0001` to the left gives us `0010`.

- Test if a certain bit is set:
	- `if ((myFlags & FLAG_ONE) == FLAG_ONE )`
- Clear a bit:
	-  `myFlags &= ~FLAG-ONE;`
		-  The `&=` is analogous to `+=`; the `~` is the complement operator. `~FLAG_ONE` is `1110`, so bitwise AND clears the value of the bit, because T & F = F. 
-  Turn on a bit:
	-  `myFlags |= FLAG_ONE;`
		-  The `|=` is a bitwise OR, so `0000 & 0001 == 0001`.

## Understanding data types

- The type determines how many bytes are allocated in memory for the data that you are entering. 

### Integers

Type|Size|Range
----|----|-----
char| 1 byte| -128 to 127, or 0-255
unsigned char| 1 byte | 0 - 255
signed char | 1 nyte | -128 to 127
signed int| 2 or 4 bytes | -32,768 to 32,767 (2bytes), -2,147,483,648 to 2,147,483,648 (4 bytes)
unsigned int| 2 or 4 bytes| 0 to 65,535 (2bytes) or 0 to 4,294,967,295 (4bytes)
short|2bytes| -32,768 to 32,767
unsigned short| 2bytes|0 to 65,535
long| 4bytes| -2,147,483,648 to 2,147,483,647
unsigned long|4bytes| 0 to 4,294,967,295

### floating point types

type|size|stored range|output precision
----|----|------------|----------------
float|4byte|1.2E-38 to 3.4E+38|6 decimal places
double|8byte|2.3E-308 to 1.7E+308|15 decimal places
long double|16byte|3.4E-4932 to 1.1E+4932|19 decimal places

### void

- no value/no data is needed
- adds clarity to code and debugging

### boolean types

- not defined in standard C
- `1` is equivalent to `TRUE`
- `0` is equivalent to `FALSE`
- a standard boolean library, since C99, has been defined called `<stdbool.h>`
- you can also use `typedef` to clean up code.

- Workaround using preprocessor directives:

````
typedef int Boolean;
#define True 1
#define False 0
````
- use `sizeof(<data type>)` to determine size on your architecture

### strings in C

- strings are stored in arrays of type `char`
- `char array[30];` defines a string of thirty `char`
- better support for strings is found in `<string.h>`
	- functions:
		- `strcmp(str1,str2)` compares two strings and returns a number result, negative if the first is longer, positive if the second is longer
		- `strcpy(dest,src)` copies `src` onto `dest`
		- `memcpy(dest,src,n)` copies `n` chars from `src` to `dest`
		- `strlen(str)` returns the length of a string. 

## Control Flow

### Conditionals

#### If / Else

```
if (__condition__){
	statement
} else{
	statement
}
```
- conditions can be chained, using boolean logic. `if( a!=0 && a < 5)`

#### switch

__switch__(*expression*){*cases*}

```
switch(i){
	case 1:
	case 2:
		printf("1 or 2\n");
		break;
	case 7:
		printf("7\n");
		break;
	default:
		printf("default value\n");
}
```

#### continue

- `continue;` can be used to conditonally avoid an iteration of a loop, e.g. to avoid a divide by zero or something

#### goto
- __goto__ can be used to jump out of a function or from a nested loop
```
goto L1;
/* whatever you like here */
L1: /* anything else */
```

### Loops

#### while

```
while(expression){
	statement
}
```

#### do/while

```
do {
	statement
} while(expression);
```

#### for

__for__(*initialize*; *check*; *update*) {
	*statement*
}

```
for(i = 0; i < 10; i++) {
	do_something;
}
```

## Functions and Returns

- C functions can return any type except arrays and other functions.
- Declaring functions (and explicit return value type) , and the types of its arguments, must be done before the function is called.
	- e.g.: *double* __function__( int *argument*);
	- by standard, *return* must be defined unless the return type is set to be *void*

- Function __definition__ follows the form __function__(int *parameter*){ __block__};


### Arguments

- Functions can receive parameters in two ways:
	- __Pass by value__:
		- Useful when you don't want to change the value of the parameters
		- C makes a local copy of these variables for the function and then operates on them, where the original values stay unchanged globally. 
	- __Pass by reference__:
		- Useful when you want the function to change the values globally
		- Pointers are used in this syntax by prefacing the variable with an asterisk. This passes only the *addresses* of the variables so the function can manipulate them directly. 
			- ` func_name( int *par1, int *par2 )`

### Prototypes
- Declaring a function before it can be used by giving information about the types of arguments it takes, *without* the action definition of the function `void func(int first, int second);`
	- n.b. the actual names of the parameters don't need to be defined, they can be specified simply as `(int, double, float)`
- Functions can be defined before or after `main()`

### recursion
- recursion is a process in which a function calls itself


## Useful methods in `stdlib`

### `<math.h>`
- functions:
	- `sqrt` should be obvious
- constants:
		- `M_PI`

### `<stdio.h>`

#### `printf`
- provides formatting features for display multiple types of data on screen
#### `scanf`

```
char userInput[9];
scanf( "%8s", userInput); // no & when assigning to an array/pointer
```
- note that `scanf` requires a `&` to indicate a memory address to write to

- as a corollary, is for taking input from the screen and terminates on whitespace
- The above reads 8 characters of user input into the variable of the same name. The `%8s` syntax, instead of just `%s`, limits the input to only 8 characters to prevent overrun. 
	- The allocation of _9_ characters in the array allows for the null terminator of the string.   
	- Warning: `scanf` breaks on whitespace
- `getchar` asks the user for a single `char`

### `string.h`

#### `strcmp`

`int strcmp( char* strA, char* strB );`

- This compares `strA` and `strB` and returns:
	-  `0` if they are the same
	-  `1` if `strA` would be sorted before `strB`
	-  `-1` if `strB` would be sorted before `strA`


## Useful idioms

### Get value of input character(s) and loop until EOF
```
#include <stdio.h>
#include <stdlib.h>

main(){
    int input_c;

    /* The Classic Bit */
    while( (input_c = getchar()) != EOF){
            printf("%c was read\n", input_c);
    }
    exit(EXIT_SUCCESS);
}
```
### taking parameters at command line

`int main( int argc, char* *argv)`

- `argc` is an `int` of the number of total arguments
- `argv` is a pointer to an array of text strings.
- So, `*argv` is the array itself. 

### pointers to NULL

- These have to be used carefully, because the OS almost always owns memory address `0`, and will kill any attempts to access it.  Assigning a variable to NULL is a way to set the value of a pointer to zero, and is shorthand for saying "I'll need memory for this soon, but not right away." 

### `malloc` an array

`int* myArray = malloc( sizeof(int) * numItems );`

- `malloc` returns a `void` pointer to a section of memory, so we assign `myArray` with type `pointer to int`

- Using `sizeof()` is important to ensure that the compiler accounts for different int sizes depending on architecture 

### `realloc` to resize an array

`void* realloc( void* originalPointer, int newSize`

- Note that this executes `free()` on `originalPointer` at the same time, so make sure not to refer to it again.


