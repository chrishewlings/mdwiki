
# bash scripting



## Bash Strict Mode

`set -euo pipefail`
`IFS=$'\n\t'`

- `set -e` instructs bash to exit upon a non-zero exit status for _any_
  subcommand
- `set -u` instructs bash to exit on reaching a variable that is not defined
- `set -o pipefail` if any command in a pipeline fails, fail all commands 
- `IFS=$'\n\t'` sets bash looping to split on newlines and tabs, not spaces



## environment variables

Variable name|Contents
-------------|--------
$BASH_VERSION| Version of bash running
$RANDOM| a random _int_


## brace expansion

- _command_ file{0001..1000} will act on file 0001, 0002, etc. without using an external command like _seq_ 

## redirects

-- `&>` is a faster way of typing `2&>1`

## brackets and escaping

- single quotes `'thing'` will __not__ expand variables
- double quotes `"thing"` __will__ expand variables
- backticks can be used for command substitution
- so can brackets, e.g. d=$(pwd)

## Arithmetic Operations

- __arithmetic operations__ should use two surrounding parens e.g. `e=$((2+2))`
- operators include *, **, ++, --, +=, -=, *=, etc. much like C
- bash also only uses integers internally. to support floats you can use input and output from `bc`

- __comparison operations__ should use two surround square braces e.g. `e=[[ "cat" == "cat" ]]

## Comparison operators

Operation|Operator
---------|--------
Less than| `[[ $a -lt $b ]]`
Greater than| `[[ $a -gt $b ]]`
Less than or equal to| `[[ $a -le $b ]]`
Greater than or equal to| `[[ $a -ge $b ]]`
Equal | `[[ $a -eq $b ]]`
Not equal | `[[ $a -ne $b ]]`

## Logical operators

Operation|Operator
---------|--------
logical AND| `[[ $a && $b ]]`
logical OR| `[[ $a || $b ]]`
logical NOT| `[[ ! $a ]]`

## String operators

Operation|Operator
---------|--------
check if null| `[[ -z $string ]]`
check if non-null| `[[ -n $string ]]`

- string length can be returned with `${$a}`
- substrings:
	- `c="helloworld"`
	- `${c:3} == loworld`
	- `${c:3:4} == lowo`
	- `${c: -4} == orld`
	- `${c: -4:3} == orl`

- search and replace:
	- `fruit="apple banana banana cherry"`
	- `${fruit/banana/pear} == "apple pear banana cherry"`
	- `${fruit//banana/pear} == "apple pear pear cherry"`
	- `#` = beginning of string
	- `%` = end of string

## Handling text

- `echo -e` implies that you will be using escape codes


## Colors
Color|Foreground|Background
-----|----------|----------
Black|30|40
Red|31|41
Green|32|42
Yellow|33|43
Blue|34|44
Magenta|35|45
Cyan|36|46
White|37|47

## styled text (ANSI)

Style|Value
-----|-----
No Style|0
Bold|1
Low Intensity|2|
Underline|4|
Blinking|5|
Reverse|7|
Invisible|8|



## dissecting an ANSI escape sequence

- `\033[` is the actual _escaped_ component that tells the shell to treat the following characters differently, terminated with `m`
- `\033[`1;_37_;__40__`m`
	- where `1` implies style `bold`
	- `37` is the _foreground_ colour (white)
	- `40` is the _background_ colour (black)

- `\033[0m` is to return to default

- Easier in practice to use variables in longer scripts. i.e.
- `whiteonblack="\033[37;40m"` and then just call `$whiteonblack` inside your statement

## tput for styling text (So much easier!)

Style|Command
-----|-------
Foreground|`tput setaf [0-7]`
Background|`tput setab [0-7]`
No Style|`tput sgv0`
Bold|`tput bold`
Low intensity|`tput dim`
Underline|`tput smul`
Blinking|`tput blink`
Reverse|`tput rev`

ex. `flashred = $(tput setab 0, tput setaf 1; tput blink)`



## printf

- `printf` allows C like string printing options and substitutions
	- `printf "Name:\t%s\nID:\t%04d\n" "Chris" "16"`
		- `%s` is a string replacement placeholder
		- `%04d` is a integer replacement placeholder that pads to 4 digits for spacing, and pads with `0`

- `printf` can also be used to print a value into a variable using the `-v <var>` syntax
- e.g. `printf -v mystring "Current User\t%s\nDate:\t\t%s @ %s\n" $USER $today $time` // renders all escape characters and subs in variables and then saves the output into `$mystring`

## Arrays
- Arrays are assigned and referred to inside `()`
	- `a=()` // empty array
	- `b=("apple" "banana" "cherry")` // filled array

Using array `$b` from above:
	- `${b|1|` == banana
	- `${b[@]` == apple banana cherry // `@` is whole array 
	- `${b[@]: -1` == cherry // ``[@]: -1` is last array element
	- `b+=("mango")` == apple banana cherry mango // appends "mango" to array

## Associative arrays (key-value pairs)
Tip: Only in bash 4+

- `declare -A myarray` will create an associative array

`myarray[color]=blue` // creates a key named `color` with a value named `blue`
`myarray["Where am I?"]="Building 4"` // use quotes to avoid whitespace issues

`echo ${myarray["color"]}` == `blue`


## Common useful script idioms

- `todays_date=$(date +"%d-%m-%Y")` // assigns date in form `dd-mm-yy` to `$todays_date`
- `current_time=$(date +"%H:%M:%S)` // assigns date in form `HH:MM:SS` to `current_time`

### reading files

```bash
i=1
while read f; do
	echo "Line $i: $f"
	((i++))
done < file.txt
```
Tip: This reads `file.txt` line by line. `i` is a loop counter, `f` corresponds to the contents of the line currently being read.

### heredocs

```bash
cat <<- EOT
	This is a
	multiline
	text string
EOT
```
Tip: the `-` is not necessary above, but it strips out the leading tab characters which improves readability. 

## declare

- `declare` operator can add attributes to variables as well
	- `declare -i d=123` declares `$d` as an integer
	- `declare -r e=456` declares `$e` as read only
	- `declare -l f="THING"` declares `$f` as "thing" (lowercase transform)
	- `declare -l f="thing"` declares `$f` as "THING" (lowercase transform)

	
## control flow

##### `if/elif/else`
```bash
if expression; then
	do_something
elif expression2; then
	do_something_else
else
	do_nothing
fi
```

##### `while`

```bash
i=0
while [ $i -le 10 ]; do
	something
	((i++))
done
```


##### `until`

```bash
i=0
until [ $i -ge 10]; do
	something
	((i++))
done
```

##### `for`

```bash
for i in 1 2 3
do
	something
done
```

##### sequences can also be used:

```bash
for i in {1..100}
do
	something_100_times
done
```

###### C style `for` loop:

```bash
for (( i=1; 1<=10; i++)
do
	c_style_loop
done
```

## looping through arrays

```bash
array=("apple" "banana" "cherry")
for i in ${array[@]}
do
	action
done
```

## looping through associative arrays

```bash
declare -A arr
arr["name"]="Chris"
id["id"]="1234"
for i in "${!arr[@]}" // using quotes to make sure strings are properly treated
do
	echo "$i : ${arr[$i]}"
done
```

## case statements

```bash
a="dog"
case $a in 
	cat) echo "Feline;; // always requires two semicolons
	dog|puppy) echo "Canine";; // using pipe allows multiple cases to have same action
	*) echo "none";; //default case
esac
```

## functions

##### no args

```bash
function greet {  
	echo "Hi there!"
}

greet
```
##### with arguments

```bash
function numberthings {
	i=1
	for f in $@; do  // $@ is an array variable with all of the arguments passed to the function
		echo $i: $f
		((i++))
	done
}
```

- _$1_, _$2_, _$n_ used for indivudal arguments to function
- _$#_ is an int with the number of arguments

## getopts

```bash
while getopts u:p:ab option; do // using colons after flag name implies it requires a value
	case $option in
		u) user=$OPTARG;; // $OPTARG is value following the flag, i.e. -f "file"
		p) pass=$OPTARG;;
		a) echo "got the -a flag";;
		b) echo "got the -a flag";;
		?) echo "unknown flag";; // default case
	esac
done
```

## getting input

- using the `read` keyword
	- `read <variable>` prompts the user for input and then writes it to _<variable>_
	- `read -s` asks in silent mode, i.e. for passwords and such

- using the `select` structure presents a menu to the user
```bash
select animal in "cat" dog" "bird" "fish"
do
	echo "you selected $animal!"
	break
done
```

## error tolerance

- checking for sufficient number of arguments
```bash
if [ $# -lt 3 ]; then
	echo "this requires three or more arguments."
fi
```

- looping until valid value

```bash
read -p "Favourite animal? " a
while [[ -z "$a" ]]; do // -z returns true if variable _does not_ exist
	read -p "please answer. " a
done
echo "$a was selected."
```
 
