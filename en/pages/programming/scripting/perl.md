#perl 

## variable types
- `$VAR` defines a basic scalar variable
- `@ARRAY` defines an array : `my @ARRAY = (foo, bar, baz)`
- `%HASH` defines a hash: `my %HASH = ( "this" -> "that", "who" -> "where")

declaring variables:

- preface with _my_ 
- variables are initialized in different ways
	- scalar (strings, ints, etc) values use the __$__ character, as in _$VAR_
	- arrays, or list variables, are specified and referred with the __@__ character
		- arrays can have any kind of content, even other variables
		- contents can be displayed using the _join_ function
		
		- `my @array = (1, 2, 3, 4)`