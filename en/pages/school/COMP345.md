[gimmick: math]()

# COMP 345 Final Review

## Intro

- Compilation unit is a file ( + any `include`d files )

- Pros:
    - General purpose
    - High performance
    - Combines high & low level flexibility
    - Almost entirely C compatible

- Cons:
    - Large and complex
    - Insecure
    - Some C++ features sacrifice performance vs C counterparts

- - - -

## Operator precedence

<table><tbody><tr><th style="text-align: left"> Precedence</th><th style="text-align: left"> Operator</th><th style="text-align: left"> Description</th><th style="text-align: left"> Associativity</th></tr><tr><th> 1</th><td> <code>::</code></td><td> Scope resolution</td><td style="vertical-align: top" rowspan="6"> Left-to-right</td></tr><tr><th rowspan="5"> 2</th><td style="border-bottom-style: none"> <code>a++</code>&nbsp;&nbsp; <code>a--</code></td><td style="border-bottom-style: none"> Suffix/postfix increment and decrement</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code><i>type</i>()</code>&nbsp;&nbsp; <code><i>type</i>{}</code></td><td style="border-bottom-style: none; border-top-style: none"> Functional cast</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>a()</code></td><td style="border-bottom-style: none; border-top-style: none"> Function call</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>a[]</code></td><td style="border-bottom-style: none; border-top-style: none"> Subscript</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>.</code>&nbsp;&nbsp; <code>-&gt;</code></td><td style="border-bottom-style: none; border-top-style: none"> Member access</td></tr><tr><th rowspan="9"> 3</th><td style="border-bottom-style: none"> <code>++a</code>&nbsp;&nbsp; <code>--a</code></td><td style="border-bottom-style: none"> Prefix increment and decrement</td><td style="vertical-align: top" rowspan="9"> Right-to-left</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>+a</code>&nbsp;&nbsp; <code>-a</code></td><td style="border-bottom-style: none; border-top-style: none"> Unary plus and minus</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>!</code>&nbsp;&nbsp; <code>~</code></td><td style="border-bottom-style: none; border-top-style: none"> bitwise NOT</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>(<i>type</i>)</code></td><td style="border-bottom-style: none; border-top-style: none"> C-style cast</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>*a</code></td><td style="border-bottom-style: none; border-top-style: none"> Indirection (dereference)</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>&amp;a</code></td><td style="border-bottom-style: none; border-top-style: none"> Address-of</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>sizeof</code></td><td style="border-bottom-style: none; border-top-style: none">Size-of</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>new</code>&nbsp;&nbsp; <code>new[]</code></td><td style="border-bottom-style: none; border-top-style: none"> Dynamic memory allocation</td></tr><tr><td style="border-top-style: none"> <code>delete</code>&nbsp;&nbsp; <code>delete[]</code></td><td style="border-top-style: none"> Dynamic memory deallocation</td></tr><tr><th> 4</th><td> <code>.*</code>&nbsp;&nbsp; <code>-&gt;*</code></td><td> Pointer-to-member</td><td style="vertical-align: top" rowspan="13"> Left-to-right</td></tr><tr><th> 5</th><td> <code>a*b</code>&nbsp;&nbsp; <code>a/b</code>&nbsp;&nbsp; <code>a%b</code></td><td> Multiplication, division, and remainder</td></tr><tr><th> 6</th><td> <code>a+b</code>&nbsp;&nbsp; <code>a-b</code></td><td> Addition and subtraction</td></tr><tr><th> 7</th><td> <code>&lt;&lt;</code>&nbsp;&nbsp; <code>&gt;&gt;</code></td><td> Bitwise left shift and right shift</td></tr><tr><th> 8</th><td> <code>&lt;=&gt;</code></td><td> Three-way comparison operator <span class="t-mark-rev t-since-cxx20">(since C++20)</span></td></tr><tr><th rowspan="2"> 9</th><td style="border-bottom-style: none"> <code>&lt;</code>&nbsp;&nbsp; <code>&lt;=</code></td><td style="border-bottom-style: none"> For relational operators &lt; and ≤ respectively</td></tr><tr><td style="border-top-style: none"> <code>&gt;</code>&nbsp;&nbsp; <code>&gt;=</code></td><td style="border-top-style: none"> For relational operators &gt; and ≥ respectively</td></tr><tr><th> 10</th><td> <code>==</code>&nbsp;&nbsp; <code>!=</code></td><td> For relational operators = and ≠ respectively</td></tr><tr><th> 11</th><td> <code>&amp;</code></td><td> Bitwise AND</td></tr><tr><th> 12</th><td> <code>^</code></td><td> Bitwise XOR (exclusive or)</td></tr><tr><th> 13</th><td> <code>|</code></td><td> Bitwise OR (inclusive or)</td></tr><tr><th> 14</th><td> <code>&amp;&amp;</code></td><td> Logical AND</td></tr><tr><th> 15</th><td> <code>||</code></td><td> Logical OR</td></tr><tr><th rowspan="7"> 16</th><td style="border-bottom-style: none"> <code>a?b:c</code></td><td style="border-bottom-style: none"> Ternary conditional</td><td style="vertical-align: top" rowspan="7"> Right-to-left</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>throw</code></td><td style="border-bottom-style: none; border-top-style: none"> throw operator</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>=</code></td><td style="border-bottom-style: none; border-top-style: none"> Direct assignment (provided by default for C++ classes)</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>+=</code>&nbsp;&nbsp; <code>-=</code></td><td style="border-bottom-style: none; border-top-style: none"> Compound assignment by sum and difference</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>*=</code>&nbsp;&nbsp; <code>/=</code>&nbsp;&nbsp; <code>%=</code></td><td style="border-bottom-style: none; border-top-style: none"> Compound assignment by product, quotient, and remainder</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>&lt;&lt;=</code>&nbsp;&nbsp; <code>&gt;&gt;=</code></td><td style="border-bottom-style: none; border-top-style: none"> Compound assignment by bitwise left shift and right shift</td></tr><tr><td style="border-top-style: none"> <code>&amp;=</code>&nbsp;&nbsp; <code>^=</code>&nbsp;&nbsp; <code>|=</code></td><td style="border-top-style: none"> Compound assignment by bitwise AND, XOR, and OR</td></tr><tr><th> 17</th><td> <code>,</code></td><td> Comma</td><td> Left-to-right</td></tr></tbody></table>


## Assorted keywords

- `auto` - internal reference in temp storage
- `volatile` - may change unexpectedly
- `register` - value is used often - compiler can refuse
- `extern` - external reference 
    - declares a function/objet which is defined later in the file or another file
    - allows global scope in c++ projects
    - compiler does not allocate memory for the variable


## Namespaces

- Unless specified, code belongs to **global** namespace.
- Every compilation unit has an unnamed, 'local' namespace

|Directive| Result|
|---------|-------|
|`using namespace <namespace>;`| Imports all, but pollutes namespace |
|`using <namespace>::<class/function>`| Imports a single module |
|`namespace myNamespace { ... } ` | User defined namespace | 
|`namespace { ... }` | (re)define things in local namespace | 

- When defining your own namespace, the `namespace myNamespace` declaration needs to be in both header and source. 
- This operator `::` is generally the scope operator. Using on its own will explicitly access global namespace, e.g. `::x` will access global version of x.

- - - -

## Functions

- A **function pointer** is a variable storing the address of the function.
- They are useful to make a **callback** mechanism, or to call a specific function on a parameter e.g. a comparator. 


```cpp

void myFunc(int x) {
    //Do Something
}

int main(void) {
    void (*funcPtr)(int) = myFunc;
    funcPtr(3);
}
```

- - - -

## Types - Primitive

### Declarations

```cpp

Type a1 {v}; // only C++11 and newer, and only works for objects, not primitives.
Type a2 = {v}
Type a3 = v;
Type a4(v);
```

- C++11 and newer: the `auto` keyword can be used for templates, iterators, etc.

### Pointers

```
int i = 69; // nice
int* ptr_i = &i; // of type pointer to int
```

|Directive|Result|
|---------|------|
|`p2 = p1`| Make `p2` point to where `p1` points|
|`*p2 = *p1`| Value pointed to by `p2` = value pointed to by `p1`|

- Useful to access `class`/`struct` members.
    + `ptr->x` is the same as `(*ptr).x` 

- If a pointer variable is within a `struct`/`class`, need to do allocation,deallocation,deep copying manually.
- Pointers to primitive types should be used only for:
    + checking equality
    + dereferencing

#### General pointer syntax

```cpp

int i = 100;
int* ptr_i = &i;

cout << &i;     // Memory address of i
cout << ptr_i;  // Memory address of i
cout << *ptr_i; // value of i
cout << &ptr_i; // Memory address of ptr_i
```

#### Pointer pitfalls: 

```cpp
int* null_ptr = NULL; // points to 0x0; dereference causes segfault
int* wild_ptr;        // points anywhere, dereference (probably) causes segfault
int* dangling_ptr = somethingDeleted; // // points anywhere, dereference (probably) causes segfault
```

### Smart Pointers

- Automated allocation,deletion, handling of dangly bits. 

|Type|Result|
|----|------|
|`std::auto_ptr`| Deprecated |
|`unique_ptr`| Single instance|
| `shared_ptr` |Use instead of `auto_ptr` |

### References

- Works like an alias. Sort of like a pointer, but:
    + No dereferencing required
    + Cannot have arrays of references
    + Can't do pointer arithmetic
    + Must be assigned on declaration. Failure to do so is a compilation error. 

### Conversions and Casting

- Implicit conversion: When a value is copied to a compatible type

| Cast type | Result | When | 
|-----------|--------|------|
| `(type) <value>`, `type (<value>)` | C-style cast |  Run time |
| `static_cast(<Type>) (expression)` | General purpose C++ cast. Bad for polymorphic types |  Compile time |
|`const_cast(<Type>) (expression)` | Remove `const` status | ? |
|`dynamic_cast(<Type>) (expression)`| Checked conversion of pointers,references. Useful for downcasting. | Run time |
|`reinterpret_cast(<Type>) (expression)`| Performs binary copy and assigns type to new value. Usually a bad idea.|

### Const

| `Const` on...       |     declaration | Result |
|---------------------|----------------|---------|
| variable name       |`const int i`,`int const i`| Variable is constant. | 
| function parameter  | `int func(const int i)` | Value of parameter cannot be changed by execution of the function.|
| method              | int func() const { ... } | Function cannot alter state of owner object.  Only methods declared as `const` can be called on a `const` object. Cannot call non-`const` methods. | 

#### Constant pointers

|Directive | Name   | Result |  
|----------|--------|--------|
| `const int* ptr` | Pointer to constant integer  | Cannot use pointer to change value pointed to | 
|`int * const ptr` | Constant pointer to integer | Cannot change where pointer points | 
|`const int * const ptr` | Constant pointer to constant inteer | Cannot change pointed-to value or pointer destination | 

#### Clockwise rule example:

Given: `const int * ptr`:

|Step|Action|Result|
|----|------|------|
|1|Start from name of variable: `ptr`| `ptr` is a ...|
|2|Move clockwise to next **pointer** or **type** : `*`| `ptr` is a pointer to ... |
|3|Keep moving clockwise to next **pointer** or **type**: `int`| `ptr` is a pointer to `int`....|
|4+|Move clockwise until hitting left hand side: `const`| `ptr` is a pointer to `int` constant|


### Static

- All static variables persist until program ends.

```cpp
int a = 1;             //Can be accessed from anywhere in file, and in other files
static int b = 2;      //Can be accessed from anywhere in file

void f() {
    static int c = 3;  // Retains value even after f ends. Initialized only once
    int d = 4;         // Local scope, no linkage.
}
```
- Member : Belongs to class as a whole
- non-member , at file scope : cannot be referred to outside of compilation unit
- non-member: value is kept even when execution goes out of its scope

- Separate declaration/definition for static constants is required.
- In ye olden days, the `enum` hack was used to make a static symbolic constant (putting only one value in an enum)

- - - -

## Types - Aggregate

### enum

- Contains named symbolic values
- default numbering from 0-n
- if an explicit value is not given, implicit numbering starts at last value given.

```c++
enum color {
    red,
    blue,
    yellow,
    green
};
```

### union

- Consists of one or more aliases for the same storage
- Useful when a single type of data can be accessed in several ways

```c++
union student {
    int id;
    char username[5];
};
```
- In above example, we can define and access student data by either id or username.

### typedefs

- Allows type names to be aliased

```c++
typedef unsigned short word; // word is now synonym for unsigned short;

typedef float rgb[3]; // rgb now synonym for array with 3 float elements;

typedef struct {
    double x,y;
} coordinate; // coordinate is now a struct with properties x,y;

coordinate p = {1,2};
```

- - - -

## Types - Array

- Declaration:
```cpp
int arr[n];
int arr2[] = {1,2,3};
int arr3[3] = {1,2,3,4} // compile time error
int arr4[5] = {1,2,3} // {1,2,3,0,0}
```

- Arrays decay to pointers:
    - `arr`: refers to first element
    - `arr+(1*sizeof(int))`: second element
    - This means that arrays can be used as parameters and returns via pointer syntax

#### Multidimensional arrays

- Passing multidimensional arrays as a parameter requires size of second,third,etc. dimensions

```cpp

int arr[3][4];

// arr[0] is a pointer to pointer to int (int**)
```

#### Dynamically allocated arrays

```cpp

int *arr;
i = new int[10];
delete [] i;
```

- Deleting a multidimensional dynamically allocated array requires `delete [] ` on its elements, then itself

- - - -

## Types - STL

- Functions can return STL containers. 

|STL Container| Associated header | What it do | Iterator? | 
|-------------|-------------------|------------|-----------|
| Vector      | `<vector>`        | Dynamically sized list type. insertion/deletion fast at end | random access | 
| Deque       | `<deque>`         | Double sided queue type | random access |
| List        | `<list>`          | Dynamically sized list type. insertion/deletion fast everywhere | bidirectional | 
| Set         | `<set>`           |  No duplicated elements | bidirectional |
| MultiSet    | `<set>`           |  Duplicated elements allowed | bidirectional |
| Map         | `<map>`           |  key value store, no duplicates | bidirectional |
| MultiMap    | `<map>`           |  key value store, duplicates |  bidirectional |   
| Stack       | `<stack>`         | LIFO | none | 
| Queue       | `<queue>`         | FIFO | none | 
| Priority Queue| `<queue>`       | highest priority element removed first | none | 
Helper functions:

| Function | Action | 
|----------|--------|
| `c1.swap(c2)` | Swap elements of `c1`,`c2` | 
| `c.max_size()`| |
| `c.clear()`   | Erases all elements|
| `c.begin()`,`c.end()` | iterators (forward order) | 
| `c.rbegin()`,`c.rend()` | iterators (reverse order)|
| `c.erase(begin,end)` | Erases elements from beginning to end | 

- Specific to vectors:

- `reserve()` : deals with spaces/allocation
- `resize()` : deals with elements/values

- - - -

## Types - Classes and Structs

- Declaration: 

```
ClassName var;                    // allocated on the stack
ClassName *var = new ClassName(); // allocated on the heap
```

### Constructors

- Classes and structs by default get:
    + Default constructor (unless **any** constructor is declared)
    + copy constructor
    + move constructor


- Copy constructor and assignment operator do member-wise shallow copy. 
- Calling virtual methods from constructors **will not do what you think** it will.
- Placement constructor replaces a current instance. 
- You can make constructors private or protected.
- Member variables are initialized **before** the constructor is called, so any object members will have their constructors called in order. 

- Derived classes call their base constructors, then their own constructors:

```cpp

class A {
public:
    A() { std::cout << "A Constructor" << std::endl; }
};

class B: public A {
public:
    B() { std::cout << "B Constructor" << std::endl; }
};

int main(void) {
    B b; 
    return 0;
}
```

output is :

- `A Constructor`
- `B Constructor`

### Destructors

- Making destructors `private` or `protected` is **almost always** a bad idea. 
- Throwing an exception from a destructor is **definitely** a bad idea. 
- On destruction, member variables are destroyed in reverse order. 
- classes get a default destructor, **unless** inheriting from a base class with a virtual destructor 
- Destructor is called **before** member variables are destroyed. 

- Derived destructors are called in reverse order from constructors. Extending the example from above:

```cpp

class A {
public:
    A() { std::cout << "A Constructor" << std::endl; }
    ~A() { std::cout << "A Destructor" << std::endl; }
};

class B: public A {
public:
    B() { std::cout << "B Constructor" << std::endl; }
    ~B() { std::cout << "B Destructor" << std::endl; }
};

int main(void) {
    B b; 
    return 0;
}
```

output is :

- `A Constructor`
- `B Constructor`
- `B Destructor`
- `A Destructor`



#### Initializer list

- Used to initialize members that are objects. Also useful for references, defaults, etc.

```cpp
ClassName::ClassName(int x, char c):
    _x = x,
    _c = c { ... }
```

### Nested and Local classes

- Public members of public inner classes can be used by outer class. 

- Local classes are within function definitions. 
- Rules:
    + Global variables declared above function can be used with scope operator: `::i`
    + static variables declared within functions can be used
    + cannot have static data members
    + enclosing functions cannot access private members of local class

### Friends

- Allows a function or class to access members designated as `private` or `protected`
- Friends are functions or classes declared as such within a class. 

- - - -

## Classes - Inheritance

- If a class is to be used polymorphically, make sure to make destructor `virtual`
- When overloading, functions cannot differ by return type alone.

- What is not inherited:
    + private members
    + constructors
    + operators
    + friends
    + destructor

- `class Derived: protected Base { ... }` : public members from base become protected
- `class Derived: private Base { ... }` : public members from base become private

- Classes can have more than one base class (multiple inheritance).
- Avoid diamond problem with virtual inheritance:

```cpp

class LivingThing {
    bool isAlive = true;
}

class Animal: virtual public LivingThing {
    int numLegs;
    void doStuff();
}

class Feline: virtual public LivingThing { 
    const int numTails = 1;
    void doStuff();
}

class Kitty: public Animal, public Feline  { 
    int cuteness = 100;
}
```

- When creating a derived object:
    - Base constructor called first
    - -> Derived1 constructor
    - -> -> Derived 2 constructor
    - -> -> -> etc.


#### Abstract classes

- **Pure virtual** : If at least one class method is declared pure virtual (i.e. `= 0`), then it's abstract.

#### Vtables

- Every class that inherits at least one virtual function is assigned a **vtable**, which is a static array of function pointers.
- Pure virtual functions mean that the vtable will contain a `NULL` pointer. 

- - - -

## Memory management

- On the heap. Allocated with `new`, deallocated with `delete`.
    - If `new` fails:
        + Pre C++98 returns `NULL`, like a failed `malloc`
        + C++98 and newer throw `bad_alloc`

- In general, every `new` should be matched with a `delete`.
    - Best to set ptr to `NULL` or `nullptr` to avoid dangling pointer issues after `delete`.  

### Stack resident values

- Size must be known at compile time
- Lifetime is limited but predictable:
    + When goes out of scope, ceases to exist

### Heap resident values
- Creation/destruction is up to programmer
- Forgetting to allocate memory will cause issues. 
- using `delete` on the same memory will cause issues. 

- - - -

## IO

### General stream behaviour

- `<iostream>`: `cin`,`cout`,`cerr`
- Overloads `<<` and `>>` operators

### Stream formatting

- Uses `<iomanip>`

```
double d = 78.5;

cout << d; // 78.5

cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(3);

cout << d; // 78.500;

cout << setprecision(5) << d; // 78.50000
```

### Files

`<fstream>`: Contains `ifstream`,`ofstream`

|Mode|Result|
|----|------|
|`ios::in`| Input | 
|`ios::out`| Output | 
|`ios::app`| Append. Creates file if doesn't exist. | 
|`ios::ate`| Output. If file exists, move to end of file. | 
|`ios::trunc`| Output. Clobbers existing file. |
|`ios::binary`| Binary input/output. | 

| Stream method | Corresponding bit | Meaning | 
|---------------|-------------------|--------|
|`eof()` | `ios::eofbit`| End of input stream is reached|
|`fail()` | `ios::failbit`,`ios::hardfail` | Stream operation has failed|
|`bad()` | `ios::badbit`| Bad bits only (invalid op|
|`good()` | `ios::goodbit`|None of the above|
|`clear()` |  | Clear all stream state flags|

- - - -

## Operator overloading

- At least one operand must be a user-defined type
- Generally better to define as free operators with `friend` access
- Good to return a `const` value to avoid confusion
- Pass by value or `const` reference

- **Stream operators** (`<<`,`>>`) can only be overloaded as free operators
    + Return stream as a reference
- **Assignment operator** (`=`) needs to return reference so multiple assignments can take place
    + Requires a self assignment check or else real bad things will happen
    + Compiler generates a shallow copy operator for assignment by default

- As **member**:
    + May use data members
    + No type conversion if used with a primitive type
- As **non-member,non-friend**:
    + Cannot access private members, necessitating accessors
- As **non-member,friend**:
    + Mentioned in class declaration
    + May use private data members
    + May have type conversion for both operands

- **Can't be overloaded**:
    + `::`
    + `.`,`.*`
    + `?`,`:`
    + `sizeof`
    + `typeid`

- Overloading `()` creates an operator function that can be passed an arbitrary number of parameters
- Overloading `->` must be a member function; sometimes used to implement smart pointers


- - - -

## Exceptions

```cpp
throw new ExceptionClassName(args);
```

- `catch` block has at most one parameter.
    - Using `(...)` as the argument to the `catch` block will catch all exceptions

- Exception in constructor: only the parts of objects that were fully constructed are destructor during stack unwinding
- `set_terminate(func)` can take a function name as parameter, to be called if a destructor throws an uncaught exception
- Any type can be thrown (even primitives like `int`)

- Exception specification clauses: (deprecated in c++11, which prefers `noexcept` instead):

```cpp
double divide(double numerator, double denominator) throw (DivideByZeroException);
```

- No guarantee that the code executed by the function will throw only those exceptions.
- If it calls something that's not a specified exception:
    - `unexpected()` is called
    - by default, `unexpected()` calls `terminate()`

- Generally bad form for constructor to throw exceptions, because it leaks memory
- Destructors should **never** be allowed to throw exceptions

### Exception types:

(n.b., all inherit from `std::exception`)

| Base Type | Derived Type | Due to... | 
|-----------|--------------|-----------|
| `std::bad_alloc` | | Out of memory calling `new` |
| `std::bad_cast` | | `dynamic_cast` failed |
| `std::bad_exception` | | Unexpected exception |
| `std::bad_typeid` | | if `typeid` parameter is `NULL` |
| `std::logic_error` | `std::domain_error`| Call is made with values outside acceptable range |
| `std::logic_error` | `std::invalid_argument`| Call is made with invalid args|
| `std::logic_error` | `std::length_error`| Size limit of object (e.g. `vector` has been exceeeded|
| `std::logic_error` | `std::out_of_range`| Value outside of range of indexed container|
| `std::runtime_error` | `std::overflow_error`|Numeric type overflow|
| `std::runtime_error` | `std::range_error`|Value out of range|
| `std::runtime_error` | `std::underflow_error`|Numeric type underflow|

### User defined exceptions

- Only particularity is the `what()` function that allows programmer to define a message
- Generally message is passed to ctor when creating exception

- - - -

## Design patterns: MVC

|Element| Function| Talks to | Website analogy| 
|-------|---------|----------|----------------|
|Model  | Manages behaviour and data of application | Controller |  Database (MySQL) | 
| View  | Renders the model to the user | Controller | HTML/CSS  |
| Controller | Receives user input | Controller, Model | PHP | 


//TODO// Example

- - - -

## Design Patterns : Creational

### Factory

- Decision making class that returns one of several possible subclasses of an abstract base class.
- **Use when**:
    + Various kinds of objects to be used polymorphically
    + Class uses hierarchy of classes to specify which object it creates
    + Class can't anticipate kind of object to create
    + Localize knowledge of which class gets created

### Abstract Factory

- Provides an interface to create and return one of several families of related objects. 
- Useful for abstracting groups of elements that may have different semantics (e.g. UIs for different windowing systems)

### Builder

- Separates construction of a complex object from its representation.
- Use when :
    + Algorithm for creating object independent of parts that make up the object
    + Construction process must allow different representations for object
    + Complex objects need to be created that have a common overall structure/interface

| Name | Type | Role | 
|------|------|------|
| `Builder` | Interface | Abstract interface for creating parts of a `Product`.|
| `ConcreteBuilder` | Class | Assembles parts of `Product` by implementing `Builder`. Defines and keeps track of created representation. | 
| `Director` | Class | Constructs a `Project` using `Builder` interface  | 
| `Product` | Class | Represents complex object under construction | 

1. Client creates `Director` object, and configures it with desired `Builder`.
2. `Director` notifies `Builder` whenever a part of the `Product` should be built.
3. `Builder` handles requests from `Director` and adds parts to `Product`.
4. Client retrieves `Product` from `Builder`.

//TODO : Example

### Prototype

- Starts with an initialized and instantiated class and copies or clones it to make new instances rather than creating new instances.
- Built on the `.clone()` method
- **When to use**:
    + When creating instances of class are time consuming or complex

- - - -

## Design Patterns : Structural

### Adapter

- Bridge beween two objects that share functionality
- Convert the interface of a class into another interface that clients expect
- **Used when**:
    - You can't change existing code

| Name | Type | Role | 
|------|------|------|
| `Target` | Interface | Defines interface that `Client` uses |
| `Adapter` | Class |Adapts `Adaptee`s interface to `Target` | 
| `Adaptee` | Interface | Defines an interface that needs adapting| 
| `Client` | Class | Colloaborated with objects conforming to `Target` interface | 

//TODO : Example


### Composite

- Treat individual objects and multiply constructed objects uniformly, i.e. treat components same regardless of complexity

### Decorator

- Can be used to add responsibilities to objects dynamically. 
- Dynamically add some data members/methods to an object at runtime

| Name | Type | Role | 
|------|------|------|
| `Component` | Interface | Abstract class representing objects to be decorated |
| `ConcreteComponent` | Class | Many subclasses that can be decorated | 
| `Decorator` | Interface | Abstract class wrapping component  | 
| `ConcreteDecorator` | Class | Different decorators adding members to component | 

//TODO : Example

- - - -

## Design Patterns : Behavioural

### Command

- Parametrize objects by the actions they perform
- Store context to support undo, rollback

| Name | Type | Role | 
|------|------|------|
| `Command` | Interface | declares interface for executing an operation |
| `ConcreteCommand` | Class | Defines binding between `Receiver` and action. implements `execute()` | 
| `Client` | Class | Creates a `ConcreteCommand` and sets its receiver  | 
| `Invoker` | Class | Asks command to carry out request | 
| `Receiver` | Class | knows how to carry out request | 

1. Client creates `ConcreteCommand` and specifies `Receiver`
2. `Invoker` stores `ConcreteCommand`
3. `Invoker` issues request via `execute()`. On failure, `ConcreteCommand` rolls back state to prior to invocation
4. `ConcreteCommand` object invokes operations on `Receiver`


### Observer

| Name | Type | Role | 
|------|------|------|
| `Subject` | Interface | Defines operations to attach/detach observer. Also called **Observable**|
| `ConcreteSubject` | Class/Model | Maintains state of observed object and notifies all observers when it changes | 
| `Observer` | Interface | Defines operations to be used to notify the registered Observers | 
| `ConcreteObserver` | Class | Attaches to a particular Subject class | 

### Strategy

 - Change behaviour of object based on conditions determined at runtime

| Name | Type | Role | 
|------|------|------|
| `ContextClass` | Class | Class that uses a certain behaviour. Contains a `Strategy` object, called through a `compute()` method |
| `StrategyAbstract` | Interface |Abstract class to be concretely defined by `Strategy`| 
| `Strategy` | Class | Provide implementation for `compute()` | 

//TODO : Example

- - - -

## Template metaprogramming

- **Metaprogramming** : writing programs that can take programs as objects to be computed
- Used in C++ for type abstract code
- Upon use of templated function in source code, compiler generates and instantiates a version of the template with given type(s)
- Fundamentally different concept to Java/C# generics, but facilitate a similar mechanism

### Method:

```cpp

template <typename T>
T max(T a, T b) {
    return a > b ? a : b;
}
```

### Operator:

```cpp

template <typename T>
std::ostream& operator<<( std::ostream& output, Stack<T> stack) {
    int i; 
    while (stack.pop(i)) {
        output << i << ' ';
    }
    return output;
}
```

### Specialization

- Defines an implementation for a specific instance of the template:

```cpp
template <>
char* max(char* a, char* b) {
    return strcmp(a,b) > 0 ? a : b;
}
```

### Class

```cpp
template <typename T> class Formatter {
    T* m_t;

public:
    Formatter(T* t) : m_t(t) {}
    void print() {
        std::cout << *m_t << std::endl;
    }
};
```

Warning: Each template class instance has its own copies of any static variables/members.

### Compilation rules

- Declare all methods as inline
- Put all methods definitions in header file with template class declaration
- Put some explicit template instantiation declarations at the end of a file (like forward declaration)
- include the `.cpp` file (not great)


## Compatibility issues

- `malloc()` and `free()` does not ensure proper construction and destruction
- C++ will not implicitly convert from a `void *`, like when using `malloc()`.

## Easy mistakes

- `*p2 = x` assigns **value of x** to value **pointed to by p2**
- `*p2 = &x` assigns **address of x** to **p2**

- `p4 = p5` : both now point to the same place
- `*p4 = *p5`: **overwrites p4** with data from p5

- `*p += 1`: Increments value.
- `*p++`: Dereference, then modifies **address** of p

- Inheriting from standard containers is a dumb fucking idea.
- if A -> B -> C, and an A& is created that actually refers to a C, then any public method of A will work on the object, even if C has tried to hide it. 

### Deleting a pointer that wasn't returned by new:

- If a pointer wasn't returned by `new`, it isn't dynamically allocated and `delete` will either attept to call a destructor a second time, or simply segfault.

### Assuming memory has been initialized

```c++
float *p1 = new float[10];
float sum;

sum += p1[0]; // p1[0] is undefined!
```


## MVC Model (Model View Controller)

Invented at PARC in 1979 for Smalltalk.
<table><tr><td>Model</td><td><ul><li>Manages behaviour and data of application.</li><li>Responds to requests for information from the view.</li><li>Responds to instructions to change state from controller.</li><li>In event-driven system, the model notifies observers (views) when they should change/react.</li></ul></td></tr><tr><td>View</td><td><ul><li>Renders the model into a form suitable for visualization/interaction.</li><li>Multiple views can exist for a single model.</li><li>The view renders the contents of a portion of the model's data.</li><li>**Push model**: View registers itself with the model for change notifications</li><li>**Pull model**: The view is responsible for calling the model when it needs to retrieve new data.</li></ul></td></tr><tr><td>Controller</td><td><ul><li>Receives user input and initiates reponses by calling on model objects.</li><li>Accepts input from user and instructs model what to do.</li><li>Translates users interactions with the view into actions to be performed by the model.</li><li>May spawn new views upon demand. </li></ul></td></tr></table>

## MVC - Creation

1. View registers as an observer on the model. 
    - Any changes to the data of the model result in a notification to the views to change state.
2. Controller is bound to a view. Actions performed on the view invoke methods in the controller.
3. Controller is given a reference to the underlying model, so that it can trigger the models behaviour functions or state change.

## MVC - User Interaction

1. View recognizes that a GUI action has taken place. 
2. In the listener method, the view calls the appropriate method on the controller.
3. The controller reponds by taking the appropriate action on the model, which may be updated. 
4. If model elements are altered, registered observed are notified of the change. 

## MVC - Observer Pattern

- Model implements the mechanics of the program
- Views are implemented as Observers that are decoupled from the Model components

- Subject: Often called "observable"
- ConcreteSubject: maintains state of observed objects and notifies observers. They are the model classes that have Views attached to them.
- Observer
- ConcreteObserver

### Behaviour

1. Client class instantiates ConcreteObservable
2. Client class instantiates and attaches concrete observers using methods from the Observable interface
3. Each time observable state changes, it notifies all attached Observers.
4. When a new Observer is added, all we need to do is instantiate it in the client class and attach it to the Observable object. 

## MVC - Better Explanation

- MVC is a paradigm for programming. 
- Separates **computation** and **data** from **interface**
- An example usage is a modern website:
    - **Model**: Database (MySQL, etc.)
    - **Controller**: Server side languages (PHP, Rails, etc.)
    - **View**: Browser, client side languages (HTML,CSS,JS)

### Model: Interacting with data

- Contains the data
- Speaks only with the controller

### View: Displaying to the user

- The interface
- Listens to input from the user (buttons, keyboard input, etc.)
- Listens to the controller

### Controller: 

- Coordinates interactions between model and view
- Process events and input to send to Model
- Transforms data to present to the View

Example: A (pseudocode) calculator application

```c++

//Model

class CalcModel {
    private:
        int x,y,sum;

    public:
        CalcModel(int x, int y) {
            sum = x+y;
        }

        int getSum() {
            return sum;
        }
};

// View

class CalcView {
    // Include fields for getting two numbers
    private:
        TextField f1,f2,result;
        GUIButton calc;

    public:
        CalcView() {
            // create a window, present widgets
            window.add(f1,f2,result,calc);
        }

        //Methods for the controller to use

        void setSolution(int z) {
            result.setText(z);
        }

        void addCalcListener(CalcListener listenCalc) {
            calc.addListener(listenCalc);
        }
};

// Controller

class CalcController {
    // Controls interaction between view and model

    private:
        CalcView v;
        CalcModel m;

    public:
        CalcController(CalcView v, CalcModel m) {
            this.v = v;
            this.m = m;

            v.addCalcListener(new CalcListener());
        }

        class CalcListener {
            public:
                void action(event e) {
                    int x,y;
                    x = v.f1;
                    y = v.f2;

                    m = new CalcModel(x,y);
                    v.setSolution(m.getSum());
                }
        };
};
```

# Pre-midterm notes

[gimmick: math]()

# COMP 345 Midterm Review

## Basics

- Can have multiple classes in a single file.
- Design/outline in `.h` or `.hpp` files, Implementation in `.cpp`.
- Free functions are allowed, unlike Java.

- - - -

## Preprocessor Directives

### Import system headers

```cpp
#include <iostream>
```

### Import user-provided headers

```cpp
#include "MyHeader.h"
```

### `ifdef`,`endif`

- Allows compile-time conditions to be evaluated. Useful when compiling for multiple platforms.

### `ifndef`

- Avoids headers from being imported multiple times.

```cpp
#ifndef MYHEADER_H
#define MYHEADER_H

void main() {
    ...
}

#endif // MYHEADER_H
```

- Another similar construct is `#pragma once`


### `define`

- Allows the preprocessor to handle constant values, or make macros:

```cpp
#define PI 3.14159
#define VAR_DUMP(x) std::cerr << #x < ": " << x << std::endl;
```

- - - -

## Operator precedence

<table><tbody><tr><th style="text-align: left"> Precedence</th><th style="text-align: left"> Operator</th><th style="text-align: left"> Description</th><th style="text-align: left"> Associativity</th></tr><tr><th> 1</th><td> <code>::</code></td><td> Scope resolution</td><td style="vertical-align: top" rowspan="6"> Left-to-right</td></tr><tr><th rowspan="5"> 2</th><td style="border-bottom-style: none"> <code>a++</code>&nbsp;&nbsp; <code>a--</code></td><td style="border-bottom-style: none"> Suffix/postfix increment and decrement</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code><i>type</i>()</code>&nbsp;&nbsp; <code><i>type</i>{}</code></td><td style="border-bottom-style: none; border-top-style: none"> Functional cast</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>a()</code></td><td style="border-bottom-style: none; border-top-style: none"> Function call</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>a[]</code></td><td style="border-bottom-style: none; border-top-style: none"> Subscript</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>.</code>&nbsp;&nbsp; <code>-&gt;</code></td><td style="border-bottom-style: none; border-top-style: none"> Member access</td></tr><tr><th rowspan="9"> 3</th><td style="border-bottom-style: none"> <code>++a</code>&nbsp;&nbsp; <code>--a</code></td><td style="border-bottom-style: none"> Prefix increment and decrement</td><td style="vertical-align: top" rowspan="9"> Right-to-left</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>+a</code>&nbsp;&nbsp; <code>-a</code></td><td style="border-bottom-style: none; border-top-style: none"> Unary plus and minus</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>!</code>&nbsp;&nbsp; <code>~</code></td><td style="border-bottom-style: none; border-top-style: none"> bitwise NOT</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>(<i>type</i>)</code></td><td style="border-bottom-style: none; border-top-style: none"> C-style cast</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>*a</code></td><td style="border-bottom-style: none; border-top-style: none"> Indirection (dereference)</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>&amp;a</code></td><td style="border-bottom-style: none; border-top-style: none"> Address-of</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>sizeof</code></td><td style="border-bottom-style: none; border-top-style: none">Size-of</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>new</code>&nbsp;&nbsp; <code>new[]</code></td><td style="border-bottom-style: none; border-top-style: none"> Dynamic memory allocation</td></tr><tr><td style="border-top-style: none"> <code>delete</code>&nbsp;&nbsp; <code>delete[]</code></td><td style="border-top-style: none"> Dynamic memory deallocation</td></tr><tr><th> 4</th><td> <code>.*</code>&nbsp;&nbsp; <code>-&gt;*</code></td><td> Pointer-to-member</td><td style="vertical-align: top" rowspan="13"> Left-to-right</td></tr><tr><th> 5</th><td> <code>a*b</code>&nbsp;&nbsp; <code>a/b</code>&nbsp;&nbsp; <code>a%b</code></td><td> Multiplication, division, and remainder</td></tr><tr><th> 6</th><td> <code>a+b</code>&nbsp;&nbsp; <code>a-b</code></td><td> Addition and subtraction</td></tr><tr><th> 7</th><td> <code>&lt;&lt;</code>&nbsp;&nbsp; <code>&gt;&gt;</code></td><td> Bitwise left shift and right shift</td></tr><tr><th> 8</th><td> <code>&lt;=&gt;</code></td><td> Three-way comparison operator <span class="t-mark-rev t-since-cxx20">(since C++20)</span></td></tr><tr><th rowspan="2"> 9</th><td style="border-bottom-style: none"> <code>&lt;</code>&nbsp;&nbsp; <code>&lt;=</code></td><td style="border-bottom-style: none"> For relational operators &lt; and ≤ respectively</td></tr><tr><td style="border-top-style: none"> <code>&gt;</code>&nbsp;&nbsp; <code>&gt;=</code></td><td style="border-top-style: none"> For relational operators &gt; and ≥ respectively</td></tr><tr><th> 10</th><td> <code>==</code>&nbsp;&nbsp; <code>!=</code></td><td> For relational operators = and ≠ respectively</td></tr><tr><th> 11</th><td> <code>&amp;</code></td><td> Bitwise AND</td></tr><tr><th> 12</th><td> <code>^</code></td><td> Bitwise XOR (exclusive or)</td></tr><tr><th> 13</th><td> <code>|</code></td><td> Bitwise OR (inclusive or)</td></tr><tr><th> 14</th><td> <code>&amp;&amp;</code></td><td> Logical AND</td></tr><tr><th> 15</th><td> <code>||</code></td><td> Logical OR</td></tr><tr><th rowspan="7"> 16</th><td style="border-bottom-style: none"> <code>a?b:c</code></td><td style="border-bottom-style: none"> Ternary conditional</td><td style="vertical-align: top" rowspan="7"> Right-to-left</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>throw</code></td><td style="border-bottom-style: none; border-top-style: none"> throw operator</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>=</code></td><td style="border-bottom-style: none; border-top-style: none"> Direct assignment (provided by default for C++ classes)</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>+=</code>&nbsp;&nbsp; <code>-=</code></td><td style="border-bottom-style: none; border-top-style: none"> Compound assignment by sum and difference</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>*=</code>&nbsp;&nbsp; <code>/=</code>&nbsp;&nbsp; <code>%=</code></td><td style="border-bottom-style: none; border-top-style: none"> Compound assignment by product, quotient, and remainder</td></tr><tr><td style="border-bottom-style: none; border-top-style: none"> <code>&lt;&lt;=</code>&nbsp;&nbsp; <code>&gt;&gt;=</code></td><td style="border-bottom-style: none; border-top-style: none"> Compound assignment by bitwise left shift and right shift</td></tr><tr><td style="border-top-style: none"> <code>&amp;=</code>&nbsp;&nbsp; <code>^=</code>&nbsp;&nbsp; <code>|=</code></td><td style="border-top-style: none"> Compound assignment by bitwise AND, XOR, and OR</td></tr><tr><th> 17</th><td> <code>,</code></td><td> Comma</td><td> Left-to-right</td></tr></tbody></table>

## Namespaces

- the `using namespace` keywords allows a bulk import of commands into the current namespace.
    - Should be avoided due to collisions.
- Can also import single commands: `using std::cin;`
- This operator `::` is generally the scope operator. Using on its own will explicitly access global namespace, e.g. `::x` will access global version of x.
- Users can define their own namespaces at will:

```c++
namespace Space1 {
    int function() {
        ...
    }
}

using namespace Space1::function;
```

- Every compilation unit (file) has implied unnamed namespace. Adding explicitly to the unnamed namespace is as simple as omitting the name following `namespace` when starting a block.
- Classes can also exist in namespaces.

- - - -

## Data Types

### Numeric

|Type|Size (bytes)|Size Range|Precision|
|----|------------|----------|---------|
|`short`|2|\\([-32767,32767]\\)| |
|`int`|4|\\([-2147483647,2147483647]\\)| |
|`long`|4|\\([-2147483647,2147483647]\\)| |
|`float`|4|[\\(~10^{-38},~10^{38})]\\)|7 digits|
|`double`|8|[\\(~10^{-308},~10^{308}\\)]|15 digits|
|`long double`|10|\\(~10^{-4932},~10^{4932}\\)]|19 digits|
|`char`|1|All ASCII characters| |
|`bool`|1|`true`,`false`| ||

- - - -

## Data Types - Primitive Arrays

- Simple aggregate data type, stored sequentially, containing elements of the same type, size fixed upon declaration.
- Good practice to use constants as sizes instead of magic numbers. Helps for readability and ease of refactoring.
- **Boost** has an `array` class that improves on static primitive arrays.

### Declaration and Access

- **Declaration**: `int score[5];`
- **Access**: `score[5]`;

### Memory Structure

In memory, an array `int a[3]` is organized:<table><tr><td>Index</td><td>0</td><td>1</td><td>2</td><td>3</td></tr><tr><td>Memory address</td><td>`a`</td><td>`a+1*sizeof(int)`</td><td>`a+2*sizeof(int)`</td><td>`a+3*sizeof(int)`</td></tr></table>

### Declaration

```c++
int a[3] = {2,3,5};
int a[3] = {2,3} // is stored as [2,3,0]
int a[] = {1,2,3} // compiler infers number of elements
int a[2] = {1,2,3} // compile time error
```

### Arrays as parameters

- When passing an array `p` to a function, note that only a **pointer** to `p` is actually passed, meaning it operates on the original array!
    - Good idea to assign it `const` to avoid issues.
    - Also an easy way that functions can be variadic. 

- Arrays **cannot** be assigned as return types, but a function can have a return type that is a pointer to get around this. 

### Multidimensional arrays

- Works just like C. Arrays can have multiple dimensions using the `a[i][j]`syntax. 
    - A two-dimensional array is stored as a pointer to an array of arrays of data elements. 

- When passing multidimensional arrays as parameters, the 2nd dimensions size must be specified, limiting their usefulness.

## Data Types - Dynamic Arrays

- Dynamically allocated arrays can be implemented using the `new` keyword, storing them on the **heap**. 
- Recall that any `new` keyword also requires a `delete` keyword!

Warning: Each element is pointed to by a pointer, so it is an **array of pointers.**

### Other implementations

- The `vector` class is a STL dynamic array type allows for automatic resizing, bounds checking, iterators, memory management. 

## Data Types - Composite types

### enum

- Contains named symbolic values
- default numbering from 0-n
- if an explicit value is not given, implicit numbering starts at last value given.

```c++
enum color {
    red,
    blue,
    yellow,
    green
};
```

### union

- Consists of one or more aliases for the same storage
- Useful when a single type of data can be accessed in several ways

```c++
union student {
    int id;
    char username[5];
};
```
- In above example, we can define and access student data by either id or username.

### typedefs

- Allows type names to be aliased

```c++
typedef unsigned short word; // word is now synonym for unsigned short;

typedef float rgb[3]; // rgb now synonym for array with 3 float elements;

typedef struct {
    double x,y;
} coordinate; // coordinate is now a struct with properties x,y;

coordinate p = {1,2};
```

## Variables

- Multiple variables can be declared on the same line: `int x,y,z`
- Declarations can take multiple forms:
    - `Type a1 {v};` - Safest, does some checking of value.
    - `Type a2 = {v};`
    - `Type a3 = v;`
    - `Type a4(v);`

- string literals are `const char[]`, not `std::string`

### keywords

`auto` - internal reference in temp storage
`volatile` - may change unexpectedly
`register` - value is used often - compiler can refuse
`extern` - external reference 
    - declares a function/objet which is defined later in the file or another file
    - allows global scope in c++ projects
    - compiler does not allocate memory for the variable


### Type checking/coercion

- Values can be coerced between types, making C++ a **weakly typed** language.
- This can have unexpected consequences. Assigning a decimal value to an `int` type will chop off everything but the integer part.

## Pointers

- For any type `t`, `t*` is of the type **pointer to t**.

- **Dereferencing**: `*p` refers to the object pointed to by the pointer `p`.
- **Address-of**: `&i` refers to the memory address of the pointer `i`.

- Like other types, pointers can be used as function parameters and as return types. 

Where `p1,p2` are pointers, `v1,v2` are values:

|Syntax|Result|
|------|------|
|`int *p1 = &v1`|Points `p1` to the location of `v1`.|
|`p2 = p1`| **Pointer assignment.** Make `p2` point to where `p1` points.|
|`*p2 = *p1`| **Value assignment.** Assigns value pointed to by `p1` to value pointed to by `p2`.|
|`p->a`| Shorthand for `*(p).a`|

In other words:

```c++
int* a_ptr = &a; // Assigns address of a to a_ptr.

value of *a_ptr is same as value of a.
value of a_ptr is the memory address of a. 
value of &a_ptr is the memory address of a_ptr.
```

- Arithmetic operators can be used on pointers, which is helpful for navigating arrays. 
    - Incrementing a pointer `p` of type `int` actually moves the pointed-to location up by `sizeof(int)`.

### Pitfalls

- We can assign a pointer any memory address, and bad bad things will happen. 
- We can also assign a typed pointer to an object of a completely different type via casting. Again, bad bad things.

#### Easy mistakes

- `*p2 = x` assigns **value of x** to value **pointed to by p2**
- `*p2 = &x` assigns **address of x** to **p2**

- `p4 = p5` : both now point to the same place
- `*p4 = *p5`: **overwrites p4** with data from p5

- `*p += 1`: Increments value.
- `*p++`: Dereference, then modifies **address** of p

#### Null pointers

- A **null** pointer stores 0 as memory address. 
- DO NOT DEREFERENCE. Segfault if you do.
```c++
int* null_p = NULL;
```

#### Wild pointer

- A **wild** pointer points to nothing in particular. Most likely a garbage value.
- wild pointer dereference may corrupt memory.

```c++
int* wild_p;
```

#### Dangling pointer

- When the object pointed to is deleted, but pointer is still pointing there
- If dereference happens, can segfault or corrupt data.

```c++
int a = 5;
int *p = &a;

free(&a);
cout << p;
```


## References

- References are essentially like an alias to a variable. They are similar to pointers, but with some limitations:
    - Cannot use pointer arithmetic.
    - Any operation applied to a reference is *actually* applied on the variable it refers to.
    - References must be initialized and declared at the same time, and cannot be changed afterwards. 

```c++
int a = 1;
int& b = a; // b is a reference to c
```

### References as function parameters

- Often simpler than function parameter passing with pointers.

```c++
void swap(int &a, int &b) {
    int tmp = a;  //Compiler knows what to do even without dereferences
    a = b;
    b = tmp;
}
```

### References as return values

- Allows a large object in memory to be returned without making a copy of it.

```c++
BigStructure& fn() {
    //do stuff
    return *bigThing;
}
```

### Caveats

- Can't have references in an array, e.g. `int& refArray[5]` is illegal.
- if A -> B -> C, and an A& is created that actually refers to a C, then any public method of A will work on the object, even if C has tried to hide it. 

## Dynamic variables

- The `new` operator creates dynamically allocated values on the **heap** that can be pointed to with pointers.
    - Does not necessarily need to be used with classes, but is more useful when done so.
- If `new` fails: 
    - Older compilers: returns `NULL`
    - Since C++98: Throws `bad_alloc` exception

- The `delete` operator destroys existing dynamic variables. Note that `delete` only is useful on pointers that were allocated by `new`!

```cpp
delete p;
p = NULL; // assign NULL to pointer to avoid leaving a dangling pointer
```

- - - -

## Memory Management

- c++ uses `new` and `delete` instead of `malloc` and `free`
- **Stack** : where all declared and initialized variables before runtime are stored.
- **Heap (free store)**: where all variables created and initialized at runtime are stored. 

#### Deleting a pointer that wasn't returned by new:

- If a pointer wasn't returned by `new`, it isn't dynamically allocated and `delete` will either attept to call a destructor a second time, or simply segfault.

#### Assuming memory has been initialized

```c++
float *p1 = new float[10];
float sum;

sum += p1[0]; // p1[0] is undefined!
```

#### Deleting a pointer twice:

```c++
int *p = new int(5);
delete p; 
...
delete p;
```

- - - -

## Constants 

- The `const` modifier has a number of different usages.

### `const` Variables

- Defining a **variable** as `const` signifies that its value cannot be changed after being initialized.

```cpp
const double PI = 3.14159;
```

### `const` Parameters

- Declaring a **parameter** as `const` means that the value of this parameter cannot be changed during the execution of the function. This is very valuable for parameters passed by reference.

```cpp
int max(const int i1, const int i2) {
    ...
}
```

### `const` Methods

- Declaring a **method** as `const` means that this function will not alter the state of the object to which it belongs.  

```cpp
int MyClass::getNum() const {
    return num;
}
```

Note: Only methods declared as `const` can be called on an object that was itself declared as `const` upon declaration!

### Summary 

|Name|Syntax|Meaning|
|----|------|-------|
|Constant variable|`const int a = 10`| `a` is a constant initialized to 10|
|Constant parameter|`void f(const int a) {...}`|`a` cannot be modified within the body of the function|
|Constant method|`void m() const{...}`|<ul><li>Cannot modify class members</li><li>Cannot call non-`const` methods</li></ul>|
|Pointer to constant int |<ul><li>`int const * ....`</li><li>`const int * ...`</li></ul>| Lets you change where it points, but not the value pointed to.|
|Constant pointer to int|`int* const ....`| Lets you change value, but not where it points. |
|Constant pointer to constant int|`int const * const`| Can change neither value or where it points.|

### Clockwise rule example:

Given: `const int * ptr`:

|Step|Action|Result|
|----|------|------|
|1|Start from name of variable: `ptr`| `ptr` is a ...|
|2|Move clockwise to next **pointer** or **type** : `*`| `ptr` is a pointer to ... |
|3|Keep moving clockwise to next **pointer** or **type**: `int`| `ptr` is a pointer to `int`....|
|4+|Move clockwise until hitting left hand side: `const`| `ptr` is a pointer to `int` constant|

- - - -

## Functions

- Functions can have default arguments:

```c++
void sort(int *arr, bool descending = false);
```

- When overloading, functions cannot differ by return type alone.

## Classes - Basics

- Classes (and structs) can be used anywhere a type can be used.
- Members are referred to using the dot notation.
- Access regulated via `public`,`private`, and `protected` specifiers. 

### `class` vs `struct`

- In C++, both work essentially the same, but `struct`s attributes are all automatically declared public, whereas `class` attributes are private. 

Warning: In a structure containing a **pointer**, then its memory allocation/deallocation must be done explicitly for that member.

- - - -

## Classes - Declaration and Access

- Objects can be declared in multiple ways:

```c++
Obj obj1;

// OR //

Obj *obj2 = new Obj();
```

- Members can also be accessed using multiple different notations:

```c++
int day1 = obj1.getNum();
int day2 = *obj2.getNum();
int day3 = obj2->getNum();
```

- - - -

## Classes - Constructors &amp; Destructors

### Constructors

- A constructor is called in one of three ways:
    - `myClass obj1;`
    - `myClass *obj2 = new myClass();`
    - `obj3 = myClass();`

- Has the same name as its class, and no return type. 
- Can have multiple constructors.
- Can include guarding conditions in constructors to ensure valid data is passed. 
- If no constructor specified, a default one is given. However, if you write any constructor then the built in one is no longer provided.
- Member variables are initialized **before** the constructor is called, so any object members will have their constructors called in order. 
- Constructor is **not necessarily public**! 

#### Initializer lists

- Can call parametrized constructors of component objects within containing class.

```c++
class coordPair {
    coordinate c1,c2;

    public:
        coordPair(int n, int m) 
          : c1(n,m), c2(n,m) {
            // do other constructor stuff//
          }
 }
```

### Destructors

- Called when:
    - Object goes out of scope
    - When the `delete` operator is explicitly called on a variable returned by `new`.

- Destructors should almost always be **virtual**, since any derived classes will need to call their own destructor, not that of the base class. 
- Destructor is called **before** member variables are destroyed. Their destructors are called bottom to top.
- Destructor is **not necessarily public**! If it's private, compile time error. 

- - - -

## Classes - Inline functions

- Inlined functions aim at optimization execution. They do so by replcing any call to this function with the functions entire code. To define a function as inline, use the `inline` prefix when defining the function.
- Inline functions are also useful for simple methods like getters and setters in the header file. 
- Similar to macros, but provide type safety.

```c++
inline int add(int a, int b) { return (a+b);}
```

- - - -

## Classes - Static members

- A `static` class member belongs to a class, not an object.
    - **Static data members** are like global variables within a class.
    - **Static functions** can only use other members declared as `static`.

- Generally initialized outside of the class declaration (except if `const`) 

- When a **non-member variable or function** is declared as `static`, it means that it cannot be referred to outside of the compilation unit it is declared in.
    - Additionally gives a variable **static duration**, meaning that its value is kept even when execution goes out of its scope.

Example: Below, the variable `c` retains its value even when `f()` is finished executing, and is only initialized once.

```cpp

int a = 1; // Can be used in other files sharing this namespace
static int b = 2; // Not accessible in other files.

void f() {
    static int c = 3;
    int d = 4;
}

cout << c ; // 3
cout << d ; // ERROR

```

- - - -

## Classes - Nested Classes, Local Classes &amp; Friends

### Nested Classes

- If `private`: Can only be used inside outer class
- If `public`: Can be used outside outer class using `OuterClass::InnerClass`

### Local Classes

- A **local class** exists within a function definition. 
- Global vairables declared above the function can be used with prefix `::`
- Static variables declared inside the function can also be used. 
- Automatic local variables cannot be used. 
- Cannot have static data members.
- Member functions must be defined inside the local classes.
- Enclosing functions cannot access private members of a local class. 

### Friends

- A **friend** function or class may access the members designated as `private` or `protected`.

- Uses the `friend` prefix on a method;
- Within class declaration, uses `friend class ClassName;`

## Classes - Inheritance

- Derived classes **do not** inherit:
    - Constructor(s)
    - Assignment operator
    - Destructor(s)
    - Friends

- When creating a derived object:
    - Base constructor called first
    - -> Derived1 constructor
    - -> -> Derived 2 constructor
    - -> -> -> etc.

- When multiple constructors are called, and then go out of scope, destructors are executed in the opposite order. 
- trying to store a derived class in a 'smaller box', e.g. `Base b = new derived()` will clobber any members of the derived class. 
    - Correct way is `Base& b = new derived()` or `Base* b = &(new derived())`

## Classes - Inheritance - Functions

- Derived classes can override base function implementations.

- **Overriding**: derived class has __exactly the same signature__
    - Overriden functions don't automatically invoke base class! No `super` method.
- **Overloading**: Two or more functions have same name with different parameter lists

### Virtual functions

- declaring a function virtual allows derived objects to apply polymorphic behaviour
- if a class contains a **pure virtual function**, it is automatically considered **abstract**.

```c++
void virtual doThing(); // regular ol' virtual fn
void virtual pure_doThing() = 0; // pure virtual fn
```
### Inherited Copy Constructors

- Copy constructor is called:
    - When instantiating one object, and initializing it with values from another object
    - When passing an object by value
    - When an object is returned by value

- With default compiler-generated copy constructor, a **shallow copy** is performed.  This means that any pointers within the object will point to the same memory space as the original objects pointers, which is usually undesirable 

### Protected and Private Inheritance

- Change `public` members in base class to `protected`:
```c++
class SalariedEmployee : protected Employee {
    ...
}
```

### Multiple Inheritance

- Classes can inherit from more than one base class:

```c++
class derivedMulti : public base1, base2 {
    ...
}
```

- Can cause the **diamond problem** if base classes have attributes with same names, caused by a derived class inheriting from two base classes that themselves share a base class:
- Resolving this requires **virtual inheritance**:

```c++
class DerivedMulti : virtual public Animal1 {
    ...
}
```

- Virtual inheritance ensures that only a single copy of a common base class is maintained in derived classes. 
- On the class that derives from both children of the base, the `virtual` keyword isn't needed. 

- - - -

## Type Casting

- C++ cast operation is checked at compile time, unlike C casting.
- There are a few different kinds of casts.

### Implicit Casting

```c++
short a = 2000;
int b;
b = a;
```

### Explicit Casting

```c++
double x = 10.3;
int y;

y = int(x); // functional notation
y = (int) x; // c notation
```

## Generic Casting

|Cast type|Result|When?|
|---------|------|-----|
|`static_cast<Type>(expr)`|General purpose casting.|Compile-time|
|`const_cast<Type>(expr)`|Casts out constant-ness| Run-time|
|`dynamic_cast<Type>(expr)`|Conversion of pointers/references within a class hierarchy, used for downcasting.| Run-time|
|`reinterpret_cast<Type>(expr)`|Performs binary copy and assigns the new type to the binary copied value. (<font color="red">VERY UNSAFE!</font>)| Run-time|

### Static casting

```cpp
static_cast<double>(intVar)
```

- Because it occurs at compile-time, it may fail at runtime if incorrect object type is passed.

### Dynamic casting

```cpp
dynamic_cast<SubClass>(SuperClassObj)
```

- Dynamic casting works on pointers
- Does runtime checking to verify successful casting.
- Deals with polymorphic types & virtual methods at runtime.

- - - -

## Smart Pointers

- Built-in `std::auto_ptr` construct to reduce chances of dangling pointers, initialization, & cleanup.
    - Prefer `std::unique_ptr` if using C++11 or newer. 

- Use `std::unique_ptr` when you don't intend to hold multiple references to the same object. 
- Use `std::shared_ptr` when you do want to refer to your object from multiple places - and do not want it to be de-allocated until all these references are themselves gone.
- Use `std::weak_ptr` when you do want to refer to your object from multiple places - for those references for which it's ok to ignore and deallocate (so they'll just note the object is gone when you try to dereference).

- - - - 

## Operator Overloading

- Most operators can be overloaded. The only ones that can't are `.`,`::`,`?:`,`sizeof`

- To allow a user-defined type to be output to a stream, one can overload the `<<` operator:

```cpp

class A {
    public:
        int i;
};

std::ostream& operator<<(std::ostream &strm, const A &a) {
    return strm << "A(" << a.i << ")";
}
```

- - - -

## Streams : Console Input/Output: <iostream>

- Contains `std::cin`,`std::cout`,`std::cerr`

## Streams: Console I/O: Output: <iomanip>

### `<iomanip>` library

|Name |Temp|Description|
|-----|----|-----------|
|`std::hex` | N | Print integers in base 16|
|`std::oct` | N | Print in base 8|
|`std::dec` | N | Print in base 10|
|`std::fixed` | N | Set fixed precision|
|`std::scientific` | N | Set scientific notation|
|`std::left` | Y | Left justify in width|
|`std::right` | Y | Right justify in width|
|`std::setw(n)` | Y | Set minimum field width|
|`std::setprecision(m)` | N | Set number of decimal places|
|`std::setfill('0')` | N | Set fill character|

### `<iomanip>` examples:

- Given: 
    - `double x = 3.1415926534;`
    - `double y = 187523.523626;`

|`floatfield`| `setprecision`| Result (`cout << x`)|Result (`cout << y`)|
|------------|---------------|---------------------|--------------------|
| Default    | Default       | `3.14159`           | `187524`           |
| Default    | `2`           | `3.1`               | `1.9e+05`          |
| Default    | `10`          | `3.141592653`       | `187523.5236`      |
|`std::fixed`| Default       | `3.14159`           | `187523.523626`    |
|`std::fixed`| `2`           | `3.14`              | `187523.52`        |
|`std::fixed`| `10`          | `3.1415926534`      | `187523.5236260000`|
|`std::scientific`| Default  | `3.141593e+00`      | `1.875235e+05`     |
|`std::scientific`| `2`      | `3.14e+00`          | `1.88e+05`         |
|`std::scientific`| `10`     | `3.1415926534e+00`  | `1.8752352363e+05` |

### Formatting output

- To format all `cout`ed values to have two digits after a decimal point:

```c++
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(2);
```

- - - -

## Streams : File Input/Output: <fstream>

```cpp
std::ifstream input("inFile.txt");
std::ifstream output("outFile.txt");
```

|Method|Result|
|------|------|
|`inFile.get()`|Gets a single character|
|`inFile.getLine()`|Gets a full line|
|`outFile.put(char)`|Writes a single character|
|`file.open("file.txt")`|Opens file from current directory|
|`file.close()`|Flushes buffer to disk and closes file handle|

### fstream

- The `fstream` object can also be used, but requires file modes to be specified:

```cpp
fstream filestream;
filestream.open("file.txt", MODE);
```

|Mode|Result|
|----|------|
|`ios::in`|Opens a file for input|
|`ios::out`|Opens a file for output|
|`ios::app`|Appends all output to end of file|
|`ios::ate`|Opens file for output. If file exists, move to end of file.|
|`ios::trunc`|Discard file contents if it already exists.|
|`ios::binary`|Opens a file for binary input/output.|

- `fstream`s have a state dictated by state bits

|State Method|State bit|Result|
|------------|---------|------|
|`eof()`| `ios::eofbit`| Returns `true` if `eofbit` is set|
|`fail()`| `ios::failbit`,`ios::hardfail`| Returns `true` if `failbit` or `hardfail` is set|
|`bad()`| `ios::badbit`| Returns `true` if `badbit` is set|
|`good()`| `ios::goodbit`| Returns `true` if `goodbit` is set|
|`clear()`| NONE | Clears all stream state flags.

- Objects can be serialized via :
    - MFC: `CObject::Serialize()`
    - Boost: `Serialization`

- - - -







