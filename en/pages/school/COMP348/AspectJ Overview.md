#AspectJ

## Join points

### General syntax

```java
<join point type> (<signature>)
```

- A **join point** is a point in the execution of the program.
- AspectJ supports join points, including *message sends* and *method execution*.
- For example, we can capture all `push` and `pop` messages sent to a `Stack` object.

- Example:
- `call(void Stack.push(String))` will capture a `push` message that:
	- is sent to a `Stack` object
	- has an argument of type `String` 
	- does not return a value

### Execution join points

- Captures the execution of a method defined in a given class. 

e.g.

```java
execution (void Server.attach(..)) // catches execution of attach, regardless of visibility.
```	

### Constructor execution join points

- AspectJ distinguishes between the execution of regular methods and of constructors. 
- Executions of constructors are identified with the `new` keyword:
	- `execution ([<modifier>] <class>.new(<parameters>)`

### Lexical structure join points

#### `within`

```java
within(<type pattern>) // Can use wildcard characters, must resolve to a class (or classes)
```

#### `withincode`

```java
withincode(<signature>) // Can use wildcard characters must resolve to a method (or methods)
```

### Control flow join points

```java
cflow(pointcut designator) // can be passed any pointcut
```

Note: `cflow(pointcut)` captures `pointcut` itself, as well as all subsequent pointcuts in its control flow.

- We can exclude `pointcut` itself, and only capture the subsequent pointcuts using the following:

```java
cflowbelow(<pointcut>)
```

### Field access join points

- Captures read and write access to fields declared in a given class.
- Signatures may contain wilcards, and must resolve to attributes of a given class. 


```java
get([<modifier>] <return type> <class>.<field>);
set([<modifier>] <return type> <class>.<field>);
```

## Pointcuts

### General Syntax

```java
pointcut <name> ([<object(s) to be picked up>]) :
                       <join point expression>
```

- A **pointcut** is a logical expression comprising multiple join points. 
- For example, a pointcut `mutators()` could combine to capture both `push` and `pop`

```java

pointcut mutators(): call(void Stack.push(String)) || call(String Stack.pop());
```

- Can be named or unnamed.

### Multiple pointcuts

- Two or more pointcuts may share join points. In that case, both advices will execute, with precedence noted in another section.

### Pointcut access modifiers

|Access modifier|result|
|---------------|------|
|`public`| Visible to all aspects, anywhere in the application.|
|No modifer| Implies that the declaration is visible to all aspects within the same package.|
|`protected`| Visible to the host aspect, and all its subaspects.|
|`private`| Visible only to the host aspect|

### Abstract pointcuts

- A pointcut can be declared abstract when we want exact behaviour to be concretely defined in subaspects.
- Expanding this idea can allow for libraries of aspects.
- Follows the same rules as abstract classes in Java.


## Advices
- An **advice** is a method-like block, associated to a pointcut, defining behaviour to be executed on a capture. 
- An advice block is never explicitly called.

- Example:

```java
before(): mutators() {
	System.out.println(">Modification message sent to stack.");
}
```

- Before the `push` or `pop` message can proceed, the `before` advice will execute.

- An advice block can be:
	- `before`: An advice running before the code associated with the pointcut
	- `after`: An advice running after the pointcut expression.
	- `around`: An advice running *instead* of the code associated with the pointcut, with a provision to resume normal execution through a `proceed` call. 

### `around` advice

- "whenever a pointcut is captured, instead of running the code associated with the pointcut, execute the body of the advice."

Warning: Unlike the other two types of advices, the `around` advice needs to contain a return type (which must be the same as the return type of the method of the associated pointcut).

- If methods have multiple return types, the type of the `around` advice should be `Object` .

### Advice precedence

#### Within same aspect

- `before`: That which is defined **earlier** in the aspect definition has precedence over the one that appears later. (executes first)
- `after`: that which is defined **later** in the aspect definition has precedence (executes last).
- `around`: the one defined first has priority.

#### From different aspects

- Where `type pattern_n` resolves to an aspect (or set of aspects):

```java
declare precedence: type pattern_1, type pattern_2 ... type pattern_n // 
```
- Precedence goes left to right.

- If there is no explicit declaration of precedence, advice from subaspects have preference over those of their parents.

Warning: if there is no expicit declaration or inheritance relationship, but an advice is defined in two separate aspects, **precedence is undefined.**

## Aspect declaration

```java
public aspect Logger {
    pointcut mutators(): call(void Stack.push(String)) || call(String Stack.pop());
    before(): mutators() {
        System.out.println(">Message sent to update stack.");
    }
}
```

## Call Join points

- Used to capture messages to objects with static type. 

e.g.

```java
call(void Server.attach(..)) // Captures mesage with zero or more arguments
```
	
|Wildcard|Meaning|
|--------|-------|
|`*`|any|
|`(..)` in parameter|Any, and of any type|
|`+` next to class name| This type, and all of its subtypes|

|Signature|Action|
|---------|------|
|`protected void Vector+.removeRange(int, int)`|Captures method calls of removeRange to a `Vector` object (or any object that inherits from it) with two `int` arguments that do not return a value.|
|`* * Vector.removeElement(Object)` | Captures removeElement call on a Vector object, of **any return type** and **any modifier**|
|`* * *.removeElement(Object)` | Captures removeElement of any Object, **any return type** and **any modifier**|
|`* * *.*(int, ..)` | Captures any method call, any return type, any modifier, any class, that takes an `int` as its first argument and **zero or more** arguments of any type.|
|`* * Vector.remove*(..)`| Captures any method whose name starts with `remove` and followed by **zero or more** character, any return type, any modifier, taking **zero or more** arguments, in class `Vector`.|

## Call to constructor join points

- The `call(Stack.new())` form captures a call to the default constructor of `Stack`.
- This can also catch messages to subtypes.

## Reflection

- AspectJ defines a special variable, `thisJoinPoint`, that contains reflective information about the current join point. 
- This will let us know which call captured the action taking place.

## Introductions

- Allows for crosscutting features (state and behaviour)
- Allows one to define a class/interface as a supertype to a given type, modifying the class hierarchy.
- Allows us to declare tht a class implements a given interface, and thus we can introduce behaviour:

```java

public interface <interface> {
	public void declare();
}

declare parents: <class> implements <interface>;
```

- We then need to define method `declare()` in `<class>`.

## Context passing

- The mechanism of *context passing* allows a pointcut to expose a binding to the underlying object, making it available to any advice that may need access.

### `this` and `target` join points

- `this` captures the sender object (caller)
- `target` captures the receiving object (callee)
- For method executions, both join points capture the executing object.

### Privileged aspects

- AspectJ allows us to get access to private features of classes, like `friend` in C++.

- Capture the execution of each method and expose a binding to the underlying object.
```java
pointcut monitoringIncs (Semaphore s):
	execution(* Semaphore.increment()) && this(s);
pointcut monitoringDecs (Semaphore s):
	execution(* Semaphore.decrement()) && this(s);
```