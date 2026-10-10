
# OPTIONS (CONT.)

| Use This Option | To Do This |
| :--- | :--- |
| `-V`, `--version` | Displays the version number of **less**. |
| `-w`, `--hiltle-unread` | Highlight the first new line after scrolling. |
| `-W`, `--HILITE-UNREAD` | Highlight the first new line after any forward movement. |
| `-X` *n*, `--tabs=`*n* | Set tab stops every *n* spaces. The default is 8. |
| `-X`, `--no-init` | Omits the termcap initialization and deinitialization strings. |
| `-Y` *n*, `--max-fs=`*n*, `w-scroll=`*n* | Scroll forward no more than *n* lines. |

# COMMANDS

| Use This Command | To Do This |
| :--- | :--- |
| `--` | Enable *option* (see the Options table in this section) using the long option form. |
| `-1` | Reverse the setting of *option* using the long option form. |
| `_option` | Display the current option setting (see the Options table in this section); specify the option using the long option form. |
| `_option` | Display the current option setting (see the Options table in this section); specify the option using the short option form (one letter). |
| `+command` | Execute *command* each time a new file is opened. |
| `--->option` | Reset *option* to the default (see the Options table in this section); specify the option using the short option form (one letter). |
| `+->option` | Reset *option* to the default (see the Options table in this section); specify the option using the short option form (one letter). |

| Use This Command | To Do This |
| :--- | :--- |
| `=`, Ctrl + G, `.f` | Show information about the file. |
| ` `, Ctrl + XX | Go to mark. |
| `\| *macro* *shell command*` | To the shell command, pipe the portion of the file from the first line on the current screen to the mark. Use `^` to indicate the beginning of the file, or `$` to indicate the end of the file. Press Enter to send the current screen. |
| `*regexp*` | Search forward for the next occurrence of the *regexp* (a regular expression). You can modify the search by entering the following at the beginning of *regexp*: |

- `^N` or `!` Search for lines that do not match the pattern.
- `^E` or `*` Search multiple files.
- `^F` or `^@` Begin the search at the first line of the first file in the command line list.
- `^K` Highlight matches but do not move to the position.
- `^R` Ignore regular expression metacharacters.

Certain characters are special as in the `**` command.

- `^N` or `!` Search for lines that do not match the pattern.
- `^E` or `*` Search multiple files. That is, if the search reaches the beginning of the current file without finding a match, the search continues in the previous file in the command line list.
- `^F` or `^@` Begin the search at the last line of the last file in the command line list, regardless of what is currently displayed on the screen or the settings of the `-*` or `-!` options.
- `^K` Same as in forward searches.
- `^R` Same as in forward searches.
- **Esc** `/+pattern` Same as `"/*."`.
- **Esc** `?+pattern` Same as `"?*."`.

| Use This Command | To Do This |
| :--- | :--- |
| `:d` | Remove the current file from the list of files. |
| `:e`, Ctrl + XV, `E` | Examine a new file. |
| `:n` | Examine the next file. |
| `:p` | Examine the previous file. |
| `:x` | Examine the first file in the command line list. |
| `?regexp` | Search backward for the next occurrence of the *regexp* (a regular expression). You can modify the search by entering the following at the beginning of *regexp*: |

- `^N` or `I` Search for lines that do not match the pattern.
- `^E` or `*` Search multiple files.
- `^F` or `@` Begin the search at the first line of the first file in the command line list.
- `^K` Highlight matches but do not move to the position.
- `^R` Ignore regular expression metacharacters.

| Use This Command | To Do This |
| :--- | :--- |
| `(` | Find the closing parenthesis when the opening parenthesis appears on the first line. |
| `)` | Find the opening parenthesis when the closing parenthesis appears on the last line. |
| `[` | Find the closing bracket when the opening bracket appears on the first line. |
| `]` | Find the opening bracket when the closing bracket appears on the last line. |
| `{` | Find the closing brace when the opening brace appears on the first line. |
| `}` | Find the opening brace when the closing brace appears on the last line. |
| `b`, Ctrl + B, Esc +v | Scroll backward one window. |
| `d`, Ctrl + D | Scroll forward one half window. |
| Enter, Ctrl + N, `e`, Ctrl + E, `]`, Ctrl + J, down arrow (↓) | Scroll forward one line. |
| `:v?` | Scroll to end of previous visual. |
| `:v?` | Scroll to end of previous visual in a column. |
| `Esc` +←, Left arrow (←) | Scroll left eight characters. |
| `Esc` +→, Right arrow (→) | Scroll right eight characters. |
| `Esc` + Ctrl + B | Prompt for two paired characters. When the second is positioned on the bottom line, search backward for the next instance of the first character. |
| `Esc` + Ctrl + F | Prompt for two paired characters. When the first is positioned on the top line, search forward for the next instance of the second character. |
| `Esc` + `π` | Repeat the previous search, going forward in the file list. |
| `Esc` + `N` | Repeat the previous search, going backward in the file list. |
| `Esc` + `s` | Scroll forward one screen. |
| `Esc` + `u` | Undo search highlighting. |
| `F` | Scroll forward and keep trying to read when the end of file is reached. |
| `g`, `.` `,` `<`, Esc + `<` | Go to the first line in the file. |
| `G`, `>`, Esc + `>` | Go to the last line in the file. |
| `h`, `H` | Show the available commands. |
| `m *mark*` | Marks the current position with *mark*, a lowercase letter. |
| `–n` | Set the default number of lines to scroll to *n*. This affects the behavior of all scrolling commands that normally scroll one window full. |
| `n` | Repeat the previous search. |
| `N` | Repeat the previous search but in the opposite direction. |
| `-l *option*` | Reverse the setting of *option* using the short option form (one letter). |
| `–*option*` | Enable *option* (see the Options table in this section) using the short option form (one letter). |

| Use This Command | To Do This |
| :--- | :--- |
| `p`, `%` | Go to a position *n* percent into the file. |
| `q`, `Q`, `:q`, `ZZ` | Quit. |
| `R` | Repaint the screen. |
| `r`, Ctrl + R, Ctrl + L | Repaint the screen. |
| `s *filename*` | Save piped input to *filename*. |
| `! *shell command*` | Run the specified shell command. You can use the following symbols for expansions: |

- `%` The name of the current file.
- `#` The name of the previous file.
- `!!` Repeats the last shell command.

| Use This Command | To Do This |
| :--- | :--- |
| `%`, `!` | (See above) |
| `SPACE`, Ctrl + V, `f`, Ctrl + F | Scroll forward one window. |
| `u`, Ctrl + U | Scroll backward one-half window. |
| `v` | Edit the current file. |
| `V` | Show the version number. |
| `y`, Ctrl + Y, Ctrl + P, `k`, Ctrl + K, up arrow (↑) | Scroll backward one line. |

# PROMPT EXPANSION

| Use This Option | To Do This |
| :--- | :--- |
| `%b< *t \| m \| b \| B \| j* >` | Display the byte offset in the current input file at one of the following lines: |

- `t` The top line.
- `m` The middle line.
- `b` The bottom line.
- `B` The next line after the bottom line.
- `j` The target line as specified by -j.

| Use This Option | To Do This |
| :--- | :--- |
| `%B` | Display the size of the current input file. |
| `%D` | Display the number of pages in the input file or, equivalently, the page number of the last line in the input file. |

| Use This Option | To Do This |
| :--- | :--- |
| `%d< *t \| m \| b \| B \| j* >` | Display the page number of one of the following lines in the input file: |

- `t` Top line.
- `m` Middle line.
- `b` Bottom line.
- `B` The next line after the bottom line.
- `j` The target line (as specified by -j).

| Use This Option | To Do This |
| :--- | :--- |
| `%E` | Display the name of the editor. |
| `%f` | Display the name of the current input file. |
| `%i` | Display the index of the current file in the list of input files. |
| `%L` | Display the line number of the last line in the input file. |
| `%d< *t \| m \| b \| B \| j* >` | Display the line number of one of the following lines in the input file: |

- `t` The top line.
- `m` The middle line.
- `b` The bottom line.
- `B` The next line after the bottom line.
- `j` The target line as specified by -j.

| Use This Option | To Do This |
| :--- | :--- |
| `%m` | Display the total number of input files. |
| `%p< *t \| m \| b \| B \| j* >` | Display the percent into the current input file at one of the following lines: |

- `t` The top line.
- `m` The middle line.
- `b` The bottom line.
- `B` The next line after the bottom line.
- `j` The target line as specified by -j.

| Use This Option | To Do This |
| :--- | :--- |
| `%s` | Display the size of the current input file. This is the same as %B. |
| `%t` | Remove trailing spaces. |
| `%x` | Display the name of the next input file in the list. |
