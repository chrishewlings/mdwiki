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

