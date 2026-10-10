
## Shell Commands, Continued

| COMMAND | DESCRIPTION |
| :--- | :--- |
| for | **variable/file** range |
| do | |
| cp $a textdir/$a | |
| done | |
| #Comment - the loop is ended | |
| **Example:** | |
| # Comment - Begin the loop | |
| for a in *.doc | |
| do | |
| commandname(s) | |
| done | |
| #Comment - The loop is ended | |
| if-then-else | The user is allowed to select from alternatives based on the result of the execution of a command. The **else** portion is optional. |
| | **Example:** |
| | # Comment - Begin the loop |
| | if |
| | commandname |
| | then |
| | commandname (alternative 1) |
| | else |
| | commandname (alternative 2) |
| | fi |
| | # Comment - The loop is ended |
| read | Read from standard input |
| shift | Shift arguments 1–9 one position to the left and decrement number of arguments |

| COMMAND | DESCRIPTION |
|---|---|
| test | Used for conditional test; has two formats: |
| | 1. $ if test expression |
| | Example: |
| | $ if test $ - -eq2 |
| | 2. $ if [expression] |
| | Example: |
| | $ if [ #-eq 2 ] |
| | Please Note: Spaces are required |
| | Operators: |
| | -eq = |
| | -lt < |
| | -le =< |
| | -ne <> |
| | -gt > |
| | -ge => |
| | String operators: |
| | = Equal |
| | != Not equal |
| | -z Zero length |
| | File status (for example, -opt file 1) |
| | -f Ordinary file |
| | -r Readable by this process |
| | -w Writable by this process |
| | -x Executable by this process |
| | -s Nonzero length |

| COMMAND | DESCRIPTION |
|---|---|
| `while loop` | Enables the user to execute (or not) a command depending on the exit status (or results) of another command |

Example:

```text
#Comment - Begin the loop
while commandname(s)
do
	commandname(s)
done
#Comment - The Loop is ended
```

## vi Editor

### Entering vi

| COMMAND | DESCRIPTION |
|---|---|
| `vi filename` | Display the specified file (in other words, bring it into the buffer) for editing |
| `vi filename1 filename2` | Edit the files consecutively (via `:n`) |
| `.exrc` | File that contains the vi profile |
| `wm=nn` | Set wrap margin to `nn` |
| `wm=nn` | Enter at a point specified other than at the first line by adding: <br> * `+` (Enter at the last line) <br> * `+ n` (Enter at line n) <br> * `+ /pattern` (Enter at the first occurrence of pattern) |
| `:n` | Next file in stack |
| `:set all` | Show all options |
| `:set nu` | Display line numbers (off when set nonu) |
| `:set list` | Display control characters in file |
| `:set wm=n` | Set wrap margin to `n` |
| `:set showmode` | Set display of the word INSERT when in insert mode |

### Reading in, Writing in, and Exiting `vi`

| COMMAND | DESCRIPTION |
| :--- | :--- |
| `:w` | Write buffer contents |
| `:w filename2` | Write buffer contents to *filename2* |
| `:w >> file2` | Write buffer contents to the end of *filename2* |
| `:q` | Quit this editing session (no writing of buffer contents if `q` is used alone) |
| `:q!` | Quit this editing session and discard any changes |
| `:r filename2` | Read *filename2* contents into buffer following the current cursor position |
| `:r! commandname` | Read the results of *commandname* shell command following the current cursor position |
| `:!` | Exit shell command (filter through command) |
| `:wq` or `ZZ` | Write buffer contents back to the file and then quit this editing session |

### Navigating in `vi`

| COMMAND | DESCRIPTION |
| :--- | :--- |
| `h`, `l` | Move one character position to the left; one character position to the right |
| `k` or `Ctrl-p` | Move the cursor to the character position immediately above the present position |
| `j` or `Ctrl-n` | Move the cursor to the character position immediately below the present position |
| `^`, `$` | Move the cursor to the beginning of the current line; to the end of the current line |
| `w`, `b` | Move the cursor one word position to the right; one word position to the left |
| `Enter` or `+` | Move the cursor to the beginning of the next line |
| `-` | Move the cursor to the beginning of the previous line |
| `G` | Move the cursor to the beginning of the last line of the buffer contents |

### Cursor Movement in vi

Can precede cursor movement commands (including the cursor arrow) with the number of times to repeat; for example, 9 <right arrow> moves right 9 characters.

| COMMAND | DESCRIPTION |
| --- | --- |
| 0 | Move the cursor to the first character in the line |
| S | Move the cursor to the last character in the line |
| ^ | Move the cursor to the first nonblank character in the line |
| fx | Move the cursor to the right to character x |
| Fx | Move the cursor to the left to character x |
| tx | Move the cursor to the right, to the character preceding x |
| Tx | Move the cursor to the left, to the character preceding x |
| w | Tab one word (nw = n tab word) (punctuation marks are considered to be words) |
| b | Backtab one word (punctuation marks are considered to be words) |
| B | Backtab one word (ignore punctuation marks) |
| e | Tab to the last character of the next word (punctuation marks are considered to be words) |
| E | Tab to the last character of the next word (ignore punctuation marks) |
| ( | Move the cursor to the beginning of the current sentence |
| ) | Move the cursor to the beginning of the next sentence |
| { | Move the cursor to the beginning of the current paragraph |
| } | Move the cursor to the beginning of the next paragraph |
| H | Move the cursor to the first line on the screen |
| M | Move the cursor to the middle line on the screen |
| L | Move the cursor to the last line on the screen |
| Ctrl-f | Scroll forward one screen |
| Ctrl-d | Scroll forward half screen |
| Ctrl-b | Scroll backward one screen |

| COMMAND | DESCRIPTION |
| :--- | :--- |
| Ctrl-u | Scroll backward half screen |
| G | Go to last line in file |
| nG | Go to line n |
| Ctrl-g | Display the current line number |

### Searching and Replacing in vi

| COMMAND | DESCRIPTION |
| :--- | :--- |
| /pattern | Search for the pattern in the forward direction |
| ?pattern | Search for the pattern in the backward direction |
| n | Continue/repeat the search in the same direction |
| N | Continue/repeat the search in the opposite direction |

### Adding Text in vi

| COMMAND | DESCRIPTION |
| :--- | :--- |
| a | Add text after the cursor (end with <Esc>) |
| A | Add text at the end of the current line (end with <Esc>) |
| i | Add text before the cursor (end with <Esc>) |
| I | Add text before first nonblank character in the current line |
| o | Add a line following the current line |
| O | Add a line before the current line |
| <Esc> | Return from insert mode to command mode |

### Deleting Text in vi

| COMMAND | DESCRIPTION |
| :--- | :--- |
| Ctrl-w | Undo entry of current word |
| @ | Kill the insert on this line |
| x | Delete the current character |

| COMMAND | DESCRIPTION |
| :--- | :--- |
| dw | Delete to the end of the current word (observe punctuation) |
| dW | Delete to the end of the current word (ignore punctuation) |
| dd | Delete the current line |
| D | Erase to the end of the same line (same as dc) |
| d) | Delete the current sentence |
| d] | Delete the current paragraph |
| dG | Delete from the current line through to the end of the buffer |
| d^ | Delete to the beginning of the line |
| u | Undo last change |
| U | Restore the current line to state it was in before the modification |

### Replacing Text in vi

| COMMAND | DESCRIPTION |
| :--- | :--- |
| ra | Replace the current character with an a |
| R | Replace all characters overwritten until <Esc> |
| s | Delete the current character and append text until <Esc> |
| s/s1/s2 | Replace s1 with s2 (but only in the same line) |
| S | Delete all the characters in the line and append text |
| cc | Replace all the characters in the line (same as s) |
| ncx | Delete n text objects of type x, where x can be: <br> w, b - words <br> ) - sentences <br> ] - paragraphs <br> § - to the end of the line <br> ^ - to the beginning of the line <br> <Enter> - append mode |
| C | Replace all the characters from the present cursor position to the end of the line |
