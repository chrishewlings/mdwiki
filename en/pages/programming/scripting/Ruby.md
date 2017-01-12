# Ruby

## Philosophies

- Everything is an object.
- Basic types (e.g. string, int, etc.) are implemented as classes. 


## Types in Ruby

### Strings

- Strings can use single quote syntax, but only double quoted strings support more advanced format strings and escape sequences. 

|Escape Sequence|Value|
|---------------|-----|
|\a|Bell Alarm|
|\???|Octal value|
|\x??|Hex Value|
|#{???}|Value of ???, where ??? is a Ruby expression|
|\e|Escape|
|\c? , \C-?|Control+?|
|\M-?|Meta-?|
|\M-\C-?|Meta-Control-?|
|\f|Form feed|
|\n|newline|
|\r|Carriage return|
|\s|Space|
|\t|Tab|
|\v|Vertical Tab|
|\b|Backspace|

Hint: You can also use strings with `%q{???}` or `%Q{???}`, for single and double quoted variants respectively. It is also possible to format multi-line strings with HEREDOC style using `<<` like in Bash.

### Numbers

#### Integers

- Ruby has two built in classes for integers: `Fixnum` and `Bignum`.
	+ `Fixnum` supports sizes between (-2^30) and (2^30 - 1), so *most* numbers you create in Ruby will be `Fixnum`.

- You can also assign and manipulate numbers in different bases:

|Prefix|Base|
|------|----|
|0b|Binary|
|0|Octal|
|0x|Hexadecimal|

#### Floating point numbers

- Ruby uses the built in `Float` type.
Hint: Ruby will only automatically assign the Float class to a variable if you specify both the decimal point and the mantissa, e.g. `1.0` instead of `1`.


### Collections of things

|Name|Syntax|Properties|
|----|------|----------|
|Range|`48..81`|Using `..` indicates an inclusive range ; using `...` instead excludes the last element.|
|

#### Ranges

Syntax: 
- `1..7` , which *includes* the final value (i.e. 0-7)
- `1...7`, which *excludes* the final value (i.e. 0-6)

Methods:

- `1..7 === 5` -> true
- `1..7.include?(10)` -> false
Hint: Both `===` and `include?` are equivalent in this context.

#### Arrays

Syntax:
- `empty = []` or `empty = Array.new`
- `filled = ['String', 1, var]`

Hint: Unlike C, arrays do not have to hold elements of the same type. 

Strings offer a useful method to array-ize their contents:
- `my_array = %w(this is a string\n)`
	+ `["this", "is", "a", "string" ]`

Hint: Like the `%q` format string for the String type, `%w` will follow single quote syntax, whereas `%W` will follow double quote syntax. 

- Arrays can also be created using the `to_a` method of some objects. e.g:
````
my_range = 1..10
my_array = my_range.to_a
-> [ 1,2,3,4,5,6,7,8,9,10 ]
````

Methods:

- You can *append* to an array by referencing a non existent member. Ruby will automatically place `nil` values as seperators if there are other unpopulated indices between the existing ones and the one you specify. More easily:
	+ You can also use the `push` method : `my_array.push($VALUE)`
	+ or the `insert` method: `my_array.insert($INDEX, VALUE)`
	+ or very simply, the `<<` operator, like Bash uses to append to a file. `my_array << 14`


	+ Accessing members:
		+ `my_array[0]`
		+ `my_array[0..2]`
		+ `my_array.at(0)`
		+ `my_array.fetch(15, "Not Found!"` - This allows you to return a default value if the index isn't found.

	+ Modifying members:
		+ `my_array.pop` will return the *last* element and remove it at the same time.
		+ `my_array.shift` will return the *first* element and remove it at the same time.
		+ `my_array.delete_at(3)` will remove the element at _index_ 3 and return its value.
		+ `my_array.delete(4)` will remove the first element with _value_ 4 and return its value.

#### Hashes

- Hashes are also called dictionaries, or associative arrays. 

Adding members: 

```
my_hash = { 'Name' => 'Chris', 'Age' => 28, 'Street' => 'Coursol' } 
```

- You can alternately create hashes using the `.new` method of the `Hash` object, and you can specify a default value as its parameter:
	+ `new_hash = Hash.new("Not found")`

Accessing members :
```
my_hash['Name'] 
-> Chris
```

- You can also access values using the `values_at` method, like arrays, by providing one or more keys. This will return the corresponding ordered values as an array.

- You can also query hashes for their contents:
- 
```
my_array.has_key?('Name')
-> True

my_array.empty?
-> False

my_array.has_value?('Drolet')
-> False
```

Other useful methods:

|Syntax|Result|Returns|
|------|------|-------|
|`my_hash.delete['key']`|Removes `value` associated to `key`|Returns `value` itself|
|`my_hash.clear`|Deletes all array keys and values.|newly empty `array`|
|`my_hash.empty?`|Returns `True` if `my_hash` has no keys or values, otherwise false||


#### Assignment, variables, etc.

- In Ruby, variables are not objects themselves, but references/pointers to items in memory. 
	+ This can have unexpected results. For example:

```
first_var = "Hello"
second_var = first_var
puts second_var
-> "Hello"
second_var.chop! #removes last character in string
puts first_var
-> "Hell" #what??
```

- If we want to pass by copy instead of passing by reference, you can use the `.clone` or `.dup` method on an object. 

- Incrementing and decrementing can be done with the `+=` and `-=` syntax: 
```
var = 2
var += 1
puts var
-> 3
```

You can also index strings via regex, with the `=~` syntax:
```
thing = "Hello World"
thing =~ /World/
-> 6
```


### Code blocks

- There are multiple ways that a block can be initiated and terminated.  Common keywords include:
	+ To define a basic block : `begin / end` 
	+ To define a **method** : `def / end` 

Hint: methods should be defined in lowercase, as Ruby uses capitalized names for **constants** and **classes**. 

_Operator conventions with methods:_

|Operator|Result|
|--------|------|
|`?`|Usually used for querying an attribute. sometimes return boolean, but not always.|
|`!`|usually modifies the object **in place**, rather than returning a changed result and leaving the original alone.|

_Methods_:

```
def addTwo(value1,value2)
	newValue = value1 + value2
end 
```
- Methods return the value of the last statement executed; i.e. the above method will return `newValue`

- Parameters can be given a default value:
```
def new_method(a = "This", b = "is", c)
	puts a + ' ' + b + ' ' + c + '.'
end
```
- Parameter lists can be variable length, using the `*` operator, which turns the variable following it into an array when interpreted:

``` 
def calculateValues(x,y,*otherValues)
	puts otherValues
end
```

