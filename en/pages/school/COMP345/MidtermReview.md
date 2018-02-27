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

## Namespaces

- the `using namespace` keywords allows a bulk import of commands into the current namespace.
    - Should be avoided due to collisions.
- Can also import single commands: `using std::cin;`
- Users can define their own namespaces at will:

```c++
namespace Space1 {
    int function() {
        ...
    }
}

using namespace Space1::function;
```

- Every compilation unit (file) has implied unnamed namespace.

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

## Variables

- Multiple variables can be declared on the same line: `int x,y,z`
- Declarations can take multiple forms:
    - `Type a1 {v};` - Safest, does some checking of value.
    - `Type a2 = {v};`
    - `Type a3 = v;`
    - `Type a4(v);`

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

- Arithmetic operators can be used on pointers, which is helpful for navigating arrays. 
    - Incrementing a pointer `p` of type `int` actually moves the pointed-to location up by `sizeof(int)`.

## References

- References are similar to pointers, but with some limitations:
    - Cannot use pointer arithmetic.
    - Any operation applied to a reference is *actually* applied on the variable it refers to.
    - References must be initialized and declared at the same time, and cannot be changed afterwards. 

## Dynamic variables

- The `new` operator creates dynamically allocated values on the **heap** that can be pointed to with pointers.
    - Does not necessarily need to be used with classes, but is more useful when done so.
- If `new` fails: 
    - Older compilers: returns `NULL`
    - Since C++98: Throws `bad_alloc` exception

- The `delete` operator destroys existing dynamic variables. 

```cpp
delete p;
p = NULL; // assign NULL to pointer to avoid leaving a dangling pointer
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

- - - -

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

- Has the same name as its class. 
- Can have multiple constructors.
- Can include guarding conditions in constructors to ensure valid data is passed. 

### Destructors

- Called when:
    - Object goes out of scope
    - When the `delete` operator is explicitly called on a pointer variable.

- - - -

## Classes - Inline functions

- Inlined functions aim at optimization execution. They do so by replcing any call to this function with the functions entire code. To define a function as inline, use the `inline` prefix when defining the function.
- Inline functions are also useful for simple methods like getters and setters in the header file. 

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

- **Overriding**: derived class has __exactly the same signature__
- **Overloading**: Two or more functions have same name with different parameter lists

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

- - - -

## Type Casting

- C++ cast operation is checked at compile time, unlike C casting.

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

## Streams and Stream Operators

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
