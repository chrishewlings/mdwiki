## Definitions


<dl>
    <dt>Imperative Programming</dt>
        <dd> - Describes programming in terms of statements that <b>change a program state</b>.</dd>
    <dt>Pure Object Oriented Programming</dt>
        <dd>- All data types are objects, and all operations are invoked by <b>message passing</b>.<dd/>
</dl>

## Variables

### Assignment

- Ruby supports assignment chaining, even within other expressions:

```ruby
a = b = 2 + 5 # both a,b = 5
a = (b = 1 + 1) + 3 # a = 5, b = 2
```

### Aliasing

- Multiple variables can refer to the same object. This is called **aliasing**:

```ruby
person1 = "James"
person2 = person1
```

- This is not a **copy**, but a reference to the same object. Changing `person1` will change `person2`, and vice versa.

## Methods

- Methods can be provided with default variables, and are variadic up to the number of parameters in the method.

```ruby
def test(a=1,b=2,c=a+b)
	puts "#{a}, #{b}, #{c}"
end

test 			# outputs 1,2,3
test 5 		# outputs 5,2,7
test 5,4		# outputs 5,4,9
test 3,4,6 	# outputs 3,4,6
test 1,2,3,4 # error
```

- Multiple values can be returned:

```ruby
def square_pair(a,b)
	return a**2, b**2
end
```

### Types

#### Naming conventions

<dl>
	<dt> Classes, Modules, Constants </dt>
		<dd> Should start with an <b>uppercase</b> letter. </dd>
	<dt> Class variables </dt>
		<dd> Start with <code>@@</code> </dd>
	<dt> Local variables, method parameters, method names</dt>
		<dd> Start with a <b>lowercase letter</b> or an <b>underscore</b></dd>
	<dt>Global variables</dt>
		<dd> Prefix with <code>@@</code> </dd>
	<dt> Instance variables </dt>
		<dd> Prefix with <code>@</code> </dd>
</dl>

```ruby
local_variable
CONSTANT_NAME
:symbol_name
@instance_variable
@@class_variable
$global_variable
ClassName
method_name
ModuleName
```

#### Classes

- Defined by the `class` keyword.
- Every class must contain an `initialize` method.

- Instantiation:  
	- `object = ClassName.new(<params>`

- Accessing class members:
	- Using the `attr_accessor :var1, var2` will implicitly define available getter/setters, retrives with `obj.var1`

### Inheritance:

- Make a descendent class:

```ruby
require "Person"
class Student < Person
	...
end
```

#### Arrays
- An array is an **ordered** collection of elements of any type.

- Creation:
	1. `a = ["hello",1,2,4.5]`
	2. `a = Array.new`

- Accessing:
	1. Exclusive range `[i...j]` :  items from i to j, **excluding** j.
	2. Inclusive range `[i..j],[i,j]` : items from i to j, **including** j.
	3. Negative indexing `[-1]` : access items counting from the end.

- Modification:
	- `a.pop` will remove & return the last element
	- `a.unshift(<item>)` will prepend an item

#### Associative Arrays (Hash)

- An **unordered** collection of elements.
- Each element is a key => value pair.
- Keys and values can be any type.

- Creation:
	- ` array = { key1 => value1, ... keyn => valuen } ` 

- Insertion: 
	- `array[<key>] = <value>`

- Deletion:
	- `array.delete_if {|k,v| k == <key>}`

- Accessing works with `[<key>]`, like arrays. 

- Iterating: 
	1. `array.each_pair do |k,v| ... end`
	2. `array.each do |k,v| ... end`
	3. `array.each {|k,v| ... }`

## Control flow

### `if`

- Form 1:

``` ruby
if <expr>
	if-body
else # optional
	else-body
end
```

- Form 2:

``` ruby
if <expr>
	if-body
elseif <expr2>
	elseif-body
else				# optional
	else-body		# 
end
```

- Form 3:
	- `if` can also be used like a lambda: `<action> if <expr>`
- Form 4: 
	- Or a ternary operator: `<expr> ? <expr1> : <expr2>` 

### `unless`

- Form 1 : 

```ruby
unless <expr> 
	unless-body
else  				# optional
	else-body		#
end
```

- Form 2 : 
	- `<expr> unless <other-expr>`

### `case`

```ruby

case item
	when val1,val2,val3
		puts "result"
	else
		# failure condition
end
```

### Classic Loops

#### Inside loops

- Skip to next iteration : `next if <expr>`
- Exit loop : `break if <expr>`
- Redo again : `redo if <expr>`

#### `while`

- Form 1:
```ruby
while <expr> do
	#something
end
```	

- Form 2:
```ruby
<expr> while <other-expr>
```

#### `until`

```ruby
until <expr> do
	#something
end
```	

- Form 2:
```ruby
<expr> until <other-expr>
```

### Iterator Loops

- `<num>.times { |count| #body }`
- `<num>.upto(<othernum>) { |count| #body }`
- `<num>.downto(<othernum>) { |count| #body }`
- `<num>step(<othernum>,<steplength>) { |count| # body }`

#### Enhanced `for` loop

```ruby
for elem in arr
	puts elem
end
```

#### `each`

`array.each { |elem| #body }`

#### `collect`

- Takes each element and passes it to a block.

```ruby
arr.collect { |x| x ** x } # returns array with squared numbers
```

#### `find`

- Returns the first element from a collection matching a condition.

```ruby
arr.find { |x| x % 2 == 0 } # returns first even number
```

## Modules

- Modules are like classes, supporting constants and methods, but:
	- **cannot be instantiated**
	- **cannot inherit** or **be inherited** 

- Often used as namespaces. 
	- A modules namespace can be added to the current one via the `include` keyword. 

- Items from modules can be used without `include` by prefixing the item with the module name. `.` for methods, `::` for constants. 

### Mixins

- Name collision is resolved via lexical ordering. The last module to be included masks all other name collisions.
- Useful for encapsulating common behaviour, but cannot be factored into a common superclass.

- Example:

```ruby

module Debugger
  def reflect
    "#{self.class.name} (\##{self.object_id}): #{self.to_s}"
  end
end

class Coordinate
  include Debugger
  attr_accessor :x, :y
  def initialize (x, y)
    @x = x
    @y = y
  end
      
  def to_s
    return "(#@x, #@y)"
  end 
end
```

## Regular Expressions

|Pattern | Description|
|-------|------------|
|`/Lisp|Lava/`| Matches a string containing Lisp, or Lava.|
|`/L(isp|ava)/`|As above.|
|`/ab+c/`|Matches a string containing an a, followed by one or more bs, followed by a c.|
`/ab*c/`|matches a string containing an a, followed by zero or more bs, followed by a c.
|
|`.`|Matches any character.|
|`/[Colloqui[um|a]/`|Matches Colloquium, or Colloquia.|

## Access Control

|Access type|Description|
|-----------|-----------|
|Public|Callable by anyone. Methods are public by default (except `initialize`).|
|Protected| Callable only by objects of the defining class and its subclasses|
|Private| Callable only in the defining class|

- Example (Form 1):

```ruby
class MyClass
  def method1 # public by default
    ...
  end
  
  protected  #protected, until specified otherwise
  def method2
    ...
  end
  
  private # private until specified otherwise
  def method3
    ... 
  end
  
  public # public until specified otherwise
  def method4
    ...
  end
end
```

- Example (Form 2):

```ruby
class MyClass
  def method1
    ...
  end
  
  public :method1, :method4
  protected :method2
  private :method3
end
```

### Introspection

- We can execute **reflective queries**
	1. What objects it contains
	2. The contents & behaviours of objects
	3. The class hierarchy


- This allows us to iterate over and inspect objects.

```ruby
ObjectSpace.each_object(ObjName) { |p|
  puts p.inspect
}
```
Output:

```ruby
#<XYZCoordinate:0x28455d8 @y=0, @z=0, @x=0>
```

#### Introspection methods

|Method|Result|
|------|------|
|`obj.respond_to?(<message>)`| Returns T/F, depending if obj responds to a message (method, var, etc)|
|`obj.id` | Returns unique ID of object.|
|`obj.class`| Returns ClassName |
|`obj.kind_of? <ClassName>`| Returns T/F if kind of obj is ClassName|
|`obj.instance_of? <ClassName>` | Returns T/F if an instance of ClassName|
|`obj.superClass` | |
|`obj.private_instance_methods`| | 
|`obj.public_instance_methods`| | 
|`obj.class_variables`| | 

