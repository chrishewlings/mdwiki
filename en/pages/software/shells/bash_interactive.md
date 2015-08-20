# Keyboard Shortcuts

- `Ctrl+xx` Toggle between the start of line and current position
- `Ctrl+x Ctrl+e` opens current line in `$EDITOR`

- `Ctrl+w` Cut word beford the cursor

- `Alt+d` Delete the word after the cursor

- `Ctrl+t` Swap the last two characters _before_ the cursor.

- `Meta+t` Swap the last two words before the cursor. 

- `Meta+u` _U_ppercase all characters from cursor to end of word.
- `Meta+l` _L_owercase all characters from cursor to end of word. 

- `Meta + .` Insert last argument of previous command. 

# Substitutions

- `!*` All arguments of previous command

# Useful one-liners

- `$ time read` - Simple stopwatch.  Kill with `EOL`

- `$ while sleep 1;do tput sc;tput cup 0 $(($(tput cols)-29));date;tput rc; done &` - Put a console clock in the top right corner.  

- `mv filename.{old,new}` - Quickly rename a file. 

- `find -not -empty -type f -printf "%s\n" | sort -rn | uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate` - Find duplicate files (first by size, then md5).
	- Hint: Only works with GNU `find`.

- `vim scp://username@host//path/to/somefile` - Use `vim` to edit a file on a remote server via SCP. 

- `du -sh * | sort -rh | head` - Find 10 largest files/folders.
	- Hint: Requires GNU `sort`.
