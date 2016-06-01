##Curses programming in Python:

- You can bootstrap the curses environment as follows:

```
import curses

screen = curses.initscr() # returns a curses window 	                   	q

screen.border(0) # Assign _screen_ a border of width 0
curses.start_color()
screen.addstr(12,25,"Hello World!") # Draw a text string at coordinates y,x
screen.refresh() # Actually commit and draw the pending operations.

screen.getch() # await input of any character
curses.endwin() # tear down the curses environment. 
```

Hint: This can also (more easily) be set up using the `curses.wrapper()` function, and calling it with the name of your `curses` function as its argument.

```
import curses

def main(screen): 
	screen.border(0)
	screen.addstr(12,25,"Hello World!")
	screen.refresh()
	screen.getch()

curses.wrapper(main)
```

does the exact same thing as the above example, but is much easier to write. 

### Useful configuration options

- `curses.noecho()` disables the automatic echoing of keys to the screen. Useful for interfaces. Disabled by `curses.noecho()`.
- `curses.cbreak()` makes applications react immediately to keystrokes, rather than requiring you to press enter. Disabled by `curses.nocbreak()`.
- `screen.keypad(True)` enables keypad mode, which returns normalized values instead of escape sequences when methods like `.getch()` are called.  
- `curses.curs_set(visibility)` sets the cursor visibility. 0, 1, 2 for invisible, visible, and emphasized, respectively. 

### Useful constants

|Constant|Use|
|--------|---|
|curses.LINES|Number of rows|
|curses.COLS|Number of columns|
|curses.ACS_VLINE|`char` representation of a vertical line|
|curses.ACS_HLINE|`char` representation of a horizontal line|



### Drawing

- the `curses.newwin(height, width, start_y, start_x)` method returns a new window instance.
- `.addstr` can accept between 1 and 4 arguments:
	+ `screen.addstr(string)`
	+ `screen.addstr(string, style)`
	+ `screen.addstr(y, x, string)`
	+ `screen.addstr(y, x, string, style)`

- `style` in the above examples can be selected from the below:
	+ `curses.A_BLINK`
	+ `curses.A_BOLD` 
	+ `curses.A_DIM`
	+ `curses.A_REVERSE`
	+ `curses.A_STANDOUT`
	+ `curses.A_UNDERLINE`

- `curses` also provides color support, using color 'pairs' 
	+ `.init_pair(number, fg, bg)` sets up a new pairing.
	+ Colors are numbered but also have built in constants to improve readability. 

|Number|Color Constant|
|------|--------------|
|0|`curses.COLOR_BLACK`|
|1|`curses.COLOR_RED`|
|2|`curses.COLOR_GREEN`|
|3|`curses.COLOR_YELLOW`|
|4|`curses.COLOR_BLUE`|
|5|`curses.COLOR_MAGENTA`|
|6|`curses.COLOR_CYAN`|
|7|`curses.COLOR_WHITE`|

- `.move(y, x)` can move the caret.

#### Menus

Draw a *horizontal* line of `n` `char`s starting at coords (`y_start, x_start`): `screen.hline(y_start, x_start, char, n)` 

Draw a *vertical* line of `n` `char`s starting at coords (`y_start, x_start`):
`screen.vline(y_start, x_start, char, n)`



### Getting Input

- `getch()` waits for a keypress and returns an ASCII code
- `getkey()` waits for a keypress and returns the character as a string, escape code, or constant, depending on the value of `curses.keypad`
- The `curses.ascii` submodule has a number of sanity checking and conversion methods from and to ASCII representation.  The built-in `ord(char)` method will convert a character to an ASCII integer representation. 
- There is also a seldom-used `curses.getstr(y, x, string_max_length)`.  More frequently, the `curses.textpad` submodule is used to get full string input.

```
import curses
import curses.textpad

def main(screen):

	editWindow = curses.newwin(5, 30, 2, 1)
	rectangle(screen, 1, 0, 7, 32)
	screen.refresh()
	
	box = Textbox(editWindow)
	box.edit() # Quit entering text with C+g, like Emacs
	
	editWindowContents = box.gather() # grab contents of the edit buffer

curses.wrapper(main)
```

