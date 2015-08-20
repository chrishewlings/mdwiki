#Javascript

##Variables

- you can define multiple variables in the same line by separating them with commas
	- strongly typed -- variable types cannot change after being defined
	- weakly typed -- variables are empty containers that can contain whatever values
	- Javascript is *weakly* typed.

##Operators

- ++, --, +=, /=, *=, -=, all valid in js
- == is equality operator , ( but also uses === as the _strict_ equality operator)
	- so == will make js act flexibly,
     e.g. `"123" == 123` will return `true`
    - BUT `"123" === 123` will return `false`

- && is and
- || is or
- parentheses can be used to enclose conditions separately

##Comments
- single line comments start with `//`
- multi line comments start/end with `/*` and `*/` respectively




##Looping & Branching

###if
````
if ( condition   ) {
_do_whatever_
} else {
_do_something_else
}
````
###switch
````
switch (variable_name) {
         case "opt1":
                   alert("butts");
                   break;
         case "opt2":
                   something();
                   break;
         case "opt3":
                   somethingElse();
                   break;
         default: alert("Invalid");
}
````
### While loop
````
while ( condition === true ) {

// do something

// increment index

}
````

### For loop

````
for ( setup index ; check condition ; increment index) {



}
````
- example: 

````
for ( var i =1 ; i < 10 ; i ++) {

// do something

}
````

### Do / While
````
do {

//something

i++;

} while (a < 10);
````


- the advantage of a do / while loop is that it will always run at least once. 


## Functions

###Defining functions without parameters
````
function myFunction() {

}
````

###defining functions with arguments and parameters
````
function addTwoNumbers(a,b) {

var result = a + b;

return result;

}
````
###distinction between parameters and arguments:

- a _parameter_ is what is passed into a function in its *definition*
- an _argument_ is what is passed into a function when it is *called*




##Built-in types

###Strings

- to convert/verify types before concatenation, you have two functions:
	- isNaN(foo) will return a bool representing validity of a number
	- Number(bar) will return a number when fed a string of a number, e.g. Number("55") returns 55



###String methods

#### Indexes

````
var phrase = "Something is happening"
var position = phrase.indexOf("is")
````
- This would define position as the starting index position in the string phrase in its first instance
	- n.b. _indexOf_ will return -1 if it does not find the substring
	- as a corollary there is a method called _.lastIndexOf_ which will give the last instance
	-

#### Substrings
- `string.slice(6,10)` will remove a substring corresponding to the index numbers that you pass as parameters. 


---- to sort ----

javascript:

confirm()
alert()
prompt()
console.log()
declare variable: var x 
ending a variable name with .length prints its string length
ending a variable name with .substring(x,y) prints the specified substring
.replace(x,y) after a string will find and replace substring x with substring y
.toUpperCase(), .toLowerCase().
assign array to variable with csv in square braces

= assigns variable
=== is equality operator

console.log

prevent function argument type errors with a simple if statement, e.g.
if (typeof(x) != 'number') return 0;


variable incrementing/decrementing
i++, i--
i+=x, i-=x will iterate by x counts



for loop context:

for( define_counter ;  condition ; iterate){code}


