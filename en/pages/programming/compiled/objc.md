# Objective C

### Preprocessor

- `#import` works just like `#include` in C.
- `#define <identifier> <value>` can be used for the preprocessor to define constants.
- Comments can be written with `//` on a single line, or `/*` `*/` on multiple lines.
- Directives:
|Directive|Description|
|---------|-----------|
|`#define`|substitutes a preprocessor macro|
|`#include`|inserts a particular header from another file|
|`#undef`|Undefines a preprocessor macro|
|`#ifdef`|Returns true if this macro is defined|
|`#ifndef`|Returns true if this macro is _not_ defined|
|`#if`|Tests if a compile time condition is true|
|`#else`|The alternative for `#if`|
|`#elif`|else and if in one statement|
|`#endif`|Ends preprocessor conditional|
|`#error`|Prints an error message on `stderr`|
|`#pragma`|Issues speial commands to the compiler using a standardized method|

#### Predefined Macros

|Macro|Description|
|`__DATE__`|Current date as character literal, in the form "MM DD YYYY"|
|`__TIME__`|Current time as character literal, in the form "HH:MM:SS"|
|`__FILE__`|Current filename as a string literal|
|`__LINE__`|Current line number as a decimal constant|
|`__STDC__`|Defined as 1 when the compiler complies with the ANSI standard|

## Syntax - Variables

### Constants

- In addition to the above-mentioned `#define` method, one can use: `const <type> <variable> = <value>`

### C-style Variables

- `extern` keyword declares a variable available during linking.

#### Integer literals

- An integer literal can have a suffix combining `u` and `l`, for unsigned and long respectively. 
- Octal integer literals can be written as `0nnn` ; hex integer literals can be written as `0xnnn`

#### Floating point literals

- Can represent in decimal form or exponential form, e.g. `1.5E3` . Like integer literals, `u` and `l` can be used here. 

#### Character & string literals

- Defined with single quotes: `char x = 'a'`
- Defined with double quotes: `"string"`

#### Arrays
- Almost exactly like C.

#### Structs

- `struct` are also exactly like C. 
- Structs can also be used as function arguments to Objective C style methods.  
- To access the members of a `struct` using a pointer to that `struct`, you can use the `->` operator:
- 
```
struct Book
{
	NSString *title;
	NSString *author;
};

struct Book firstBook;
firstBook.title = @"Paradise Lost";
firstBook.author = @"John Milton";


struct Book *structPtr;
structPtr = &firstBook;
NSString title = structPtr->title;
```

##### Bitfields

```
struct bitFieldStruct {
unsigned int flag1:1;
unsigned int flag2:1;
unsigned int flag3:1;
unsigned int flag4:1;
unsigned int fourBitValue:4;
} pack;
```

#### Pointers

- Using pointers like not an idiot:
	1) Define a pointer variable. `int *p;`
	2) Assign the _address_ of a variable to a pointer. `var = 20; p = &var;` 
	3) Access the value at the address that the pointer targets: `return *p;`
	
- It's best to initialize a pointer to `NULL` until you're ready for it to point to something.
	- You can check if a pointer points to `NULL` with an `if` statement: `if(ptr)` succeeds if ptr is not `NULL`. 





### NextStep-style types
- `NSNumber`, `NSString`, `NSMutableString`, `NSInteger`

#### NSString

`NSString *greeting = @"Hello";`

##### NSString Methods

`(NSString *)capitalizedString;`
Returns a capitalized representation of the receiver.

`(unichar)characterAtIndex:(NSUInteger)index;`
Returns the character at a given array position.

`(double)doubleValue;`
Returns the floating-point value of the receiver’s text as a double.

`(float)floatValue;`
Returns the floating-point value of the receiver’s text as a float.

`(BOOL)hasPrefix:(NSString *)aString;`
Returns a Boolean value that indicates whether a given string matches the beginning characters of the receiver.

`(BOOL)hasSuffix:(NSString *)aString;`
Returns a Boolean value that indicates whether a given string matches the ending characters of the receiver.

`(id)initWithFormat:(NSString *)format ...;`
Returns an NSString object initialized by using a given format string as a template into which the remaining argument values are substituted.

`(NSInteger)integerValue;`
Returns the NSInteger value of the receiver’s text.

`(BOOL)isEqualToString:(NSString *)aString;`
Returns a Boolean value that indicates whether a given string is equal to the receiver using a literal Unicode-based comparison.

`(NSUInteger)length;`
Returns the number of Unicode characters in the receiver.

`(NSString *)lowercaseString;`
Returns lowercased representation of the receiver.

`(NSRange)rangeOfString:(NSString *)aString;`
Finds and returns the range of the first occurrence of a given string within the receiver.

`(NSString *)stringByAppendingFormat:(NSString *)format ...;`
Returns a string made by appending to the receiver a string constructed from a given format string and the following arguments.

`(NSString *)stringByTrimmingCharactersInSet:(NSCharacterSet *)set;`
Returns a new string made by removing from both ends of the receiver characters contained in a given character set.

`(NSString *)substringFromIndex:(NSUInteger)anIndex;`
Returns a new string containing the characters of the receiver from the one at a given index to the end.

#### "Casting" between C style and NS style

`+ (NSNumber *)numberWithBool:(BOOL)value`
Creates and returns an NSNumber object containing a given value, treating it as a BOOL.

`+ (NSNumber *)numberWithChar:(char)value`
Creates and returns an NSNumber object containing a given value, treating it as a signed char.

`+ (NSNumber *)numberWithDouble:(double)value`
Creates and returns an NSNumber object containing a given value, treating it as a double.

`+ (NSNumber *)numberWithFloat:(float)value`
Creates and returns an NSNumber object containing a given value, treating it as a float.

`+ (NSNumber *)numberWithInt:(int)value`
Creates and returns an NSNumber object containing a given value, treating it as a signed int.

`+ (NSNumber *)numberWithInteger:(NSInteger)value`
Creates and returns an NSNumber object containing a given value, treating it as an NSInteger.

`- (BOOL)boolValue`
Returns the receiver's value as a BOOL.

`- (char)charValue`
Returns the receiver's value as a char.

`- (double)doubleValue`
Returns the receiver's value as a double.

`- (float)floatValue`
Returns the receiver's value as a float.

`- (NSInteger)integerValue`
Returns the receiver's value as an NSInteger.

`- (int)intValue`
Returns the receiver's value as an int.

`- (NSString *)stringValue`
Returns the receiver's value as a human-readable string.

#### NSArray

## Syntax - Functions/Methods

### Functions

- Functions need to be declared with a return type, like C/C++.

### Declaring/Defining a C style function
- Exactly like it sounds....

### Declaring/Defining an Objective-C style method

#### Declaration

```
@interface DemoClass:NSObject

- (int) addTwo:(int) num1 secondNumber:(int) num2;

@end
```

#### Definition

```
@implementation DemoClass

- (int) addTwo:(int) num1 secondNumber:(int) num2
{
	int result = num1 + num2;
	return result;
}

@end
```

#### Calling an Objective-C style method

```
// Create and instance of the methods' parent class:
DemoClass *example = [[DemoClass alloc]init];
int returnValue = [example addTwo:13 secondNumber:22]
```

## Syntax - Classes and blocks

### Declaring a block
`<returntype> (^blockName)(argumentType);`
e.g. :
```
void (^simpleBlock)(void) = ^{
	NSLog(@"This is a simple block.");
};
```
- Then the block can be invoked with `simpleBlock();`, just like a function. 

### Declaring a block with variables:
```
<returntype> (^blockName)(argumentTypes) = 
	^(int firstValue, int secondValue) {
		return blah;
	};
```

### Declaring a block with typedef

```
#import <Foundation/Foundation.h>

typedef void (^CompletionBlock)();
@interface SampleClass:NSObject
- (void)performActionWithCompletion:(CompletionBlock)completionBlock;
@end

@implementation SampleClass

- (void)performActionWithCompletion:(CompletionBlock)completionBlock{

    NSLog(@"Action Performed");
    completionBlock();
}

@end

int main()
{
    /* my first program in Objective-C */
    SampleClass *sampleClass = [[SampleClass alloc]init];
    [sampleClass performActionWithCompletion:^{
        NSLog(@"Completion is called to intimate action is performed.");
    }];
    
    return 0;
}
```
## Syntax - Flow Control

### Loop types

- `while`, `for`, `do...while`, all just like C. 

### Conditional types

- `if`, `if...else`, `switch`, again, just like C. 
- Additionally, conditional ternary operator `?`:
	+ `<Exp1> ? <Exp2> : <Exp3>`
	+ `<Exp1>` is evaluated.
		+ If `<Exp1>` is true, `<Exp2>` is returned.
		+ If `<Exp1>` is false, `<Exp3>` is returned.