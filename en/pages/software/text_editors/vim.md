

# commands

## Movement

`w` : move forward word
`b` : move back word
`e` : end of current or next word

`(` : back one sentence
`)` : forward one sentence

`{` : backward a paragraph
`}` forward a paragraph

`^` : beginning of line
`$` : end of line
`1G` : First line
`G` : last line
`(n)G`: line n of file
`%` : matching paren/brace
`[Ctrl] - e, y` : scroll the screen down and up
`[ctrl] d` : scroll down half screen
`[ctrl] u` : scroll up half screen
`[ctrl] b,f` : back and forward a whole screen
`[ctrl]+g`: displays file progress

`[shift]+ZZ` : quick quit

## Changing modes/Editing

`i` insert before cursor
`I` insert at beginning of line
`a` append after cursor
`A` append at EOL
`o` open a new line below
`O` open a new line above

`x` delete under cursor
`dd` delete entire line
`dw` delete current word
`d^` delete from cursor to beginning of line
`d$` delete from cursor to end of line

`r` - replace current character but remain in command mode
`[shift] R` - overwrite mode
`~` - change case of letter
`[shift] J` - remove next newline

`>>` indents
`<<` outdents

Tip: These, and almost any command, can be combined with numbers, i.e 3 >> to indent the next three lines 


## Copying and Pasting

`yy` yank entire line
`y5` yank 5 lines

## Searching

`/text` searches forward
`?text` searches backward
`n` repeats previous search
`N` repeats previous search in opposite direction
`*` finds next instance of text under caret
`#` finds prev instance of text under caret

## Regexes reference

`.` matches any single character
`^string` match beginning of line
`string$` match end on line

`[]` character set
	ex. `/a[xyz]c` matches axc, ayc, azc 

`[a-z]` any lowercase letter
`[A-Za-z]` any letter
	
`*` zero or more instances of the preceding character

`/<.*>` matches `<i>italic text</i>` (ignoring the first terminator and searching the rest of the line, this is called a greedy search

Tip: to avoid this:
`/<[^>]*>`

`[^>]*` signifying any character except >, zero or more times

## Search and Replace

`:s/old/new/` replaces first old with new on current line
`:s/old/new/g` replaces all olds with new on current line
`:%s/old/new/` replaces all olds with new in entire file

`/` can actually be any character.

within new string:
`&` is replaced with the found text



# Colon Commands

`:w` write without quitting
`:q` quit without writing
`:q!` abandon changes
`:vi` edit another file
`:n` go to next open file
`:p` go to previous open file
`:rew` rewind to first file
`:r` read file into this one

`:se ai` enables autoindent; :se noai disables it
`:se wm=<NUM>` enables word wrap; :se wm 0 disables it

#Configuration files

`.exrc` and `.vimrc`

you can insert colon commands in these files to change settings globablly instead of per session, although _without_ a colon. 

# External commands

## Filtering text through shell commands

`!!` filters current line through shell command
`5!!` filters current line and next 4 lines
`n!!` filters n lines
`!%` filters to matching paren
`!}` filters next paragraph
`!{` filters prev paragraph

## Using line ranges with commands

`:line, line <command>`

`:1,.` from first line to current
`:.,$` from current line to end of file

`:/foo/,/bar/ ! <command>` // searches inclusively from foo to bar and performs <command> on the text between them


