#notes on PHP
--

## General & Structure
- inside html, `<? php block ?> `
- lines terminate with `;`
- all variables begin with `$`
- comments use two forward slashes `//`

## data types

- variable type is inferred for str, int, float
- array defined by array(obj1, obj2, obj..n), and accessed by $array[n] or $array{n}
	- items can be removed with unset($array[n]);

## Control flow

#### if/else
```php
if (condition) {
block} else { 
block}
```

#### Switch

```php
switch (condition) {
	case condition:
		break;
	default:
		break;
}
```
- switch can also be called with __switch__ (*condition*): and terminated with __endswitch;__

#### For loop

```php
for($initial, end, iterator){ 
block
}
```

#### While loop
```php
while(condition) {
block
}
```

#### do/while loop
```php
do{
block}while(condition)
```

##Common commands 

- __echo__ *"string"*  -- displays text 
	- concatenation is done with `.` e.g. "this " `.` "is" `.` "valid" === "this is valid"

## String Manipulation

- __strlen__(*string*) - returns string length in characters
- __substr__(*string*, *start*, *end*)
- __strtoupper__(*string*)/__strtolower__(*string*)
- __strpos__(*haystack*, *needle*) - returns the index of the first character, or false if not found


