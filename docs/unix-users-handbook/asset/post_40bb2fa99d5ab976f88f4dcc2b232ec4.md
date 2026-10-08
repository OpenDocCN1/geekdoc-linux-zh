
of the current line for that character, and moves the cursor to it if found. A preceding count repeats the action that many times.

+   h
Move the cursor one character to the left (same as ^H). A preceding count repeats the effect.

+   i
Enter input mode, inserting the entered text before the cursor (see a).

+   j
Move the cursor one line down in the same column (same as ^J and ^N).

+   k
Move the cursor one line up (same as ^P).

+   l
Move the cursor one character to the right (same as \ ).

+   mx
Mark the current position of the cursor. x is a lowercase letter, a-z, that is used with the ` and ' commands to refer to the marked line or line position.

+   n
Repeat the last / or ? scanning commands.

+   o
Open a line below the current line and enter input mode; otherwise like O.

+   p
Put text after/below the cursor; otherwise like P.

+   r
Must be followed by a single character; the character under the cursor is replaced by the specified one. (The new character can be a new-line.) If r is preceded by a count, count characters are replaced by the specified character.

+   s
Delete the single character under the cursor and enter input mode; the entered text replaces the deleted character. A preceding count specifies how many characters on the current line are changed. The last character being changed is marked with a $, as for c.

+   t
Must be followed by a single character; scan the remainder of the line for that character. The cursor moves to the column prior to the character if the character is found. A preceding count is equivalent to repeating the search count times.

+   u
Reverse the last change made to the current buffer. If repeated, u alternates between these two states; thus is its own inverse. When used after an insertion of text on more than one line, the lines are saved in the numerically named buffers.

+   w
Move forward to the beginning of the next word (where word is defined as in b). A preceding count specifies how many words the cursor advances.

+   x
Delete the single character under the cursor. When x is preceded by a count, x deletes the specified number of characters forward from the cursor position, but only on the current line.

+   y
Must be followed by a movement command; the specified text is copied (yanked) into the unnamed temporary buffer. If preceded by a named buffer specification, "x", the text is placed in that buffer also. If the command is yy, the entire current line is yanked.

### z
Redraw the screen with the current line placed as specified by the following options: z:center specifies the top of the screen, z. the center of the screen, and z- the bottom of the screen. The commands z^ and z+ are similar to ^B and ^F, respectively. However, z^ and z+ do not attempt to maintain two lines of overlap. A count after the z and before the following character to specifies the number of lines displayed in the redrawn screen. A count before the z gives the number of the line to use as the reference line instead of the default current line.

## Keyboard Editing Keys

At initialization, the editor automatically maps some terminal keyboard editing keys to equivalent visual mode commands. These mappings are only established for keys that are listed in the following table and defined in the terminfo(4) database as valid for the current terminal (as specified by the TERM environment variable).

Both command and input mode mappings are created (see map command in ex(1)). With the exception of the insertchar keys, which simply toggle input mode on and off, the input mode mappings exit input mode, perform the same action as the command mode mapping, and then reenter input mode.

On certain terminals, the character sequence sent by a keyboard editing key, which is then mapped to a visual mode command, can be the same character sequence a user might enter to perform another command or set of commands. This is most likely to happen with the input mode mappings; therefore, on these terminals, the input mode mappings are disabled by default. Users can override the disabling and enabling of both the command and input mode keyboard editing key mappings by setting the keyboardedit and keyboardedit! editor options as appropriate (see ex(1)). The timeout, timeoutlen, and doubleescape editor options are alternative methods of addressing this problem.

| terminfo entry | command mode map | input mode map | map name | description |
| :--- | :--- | :--- | :--- | :--- |
| key_ic | i | ^[ | inschar | insert char |
| key_eic | i | ^[ | inschar | end insert char |
| key_up | k | ^[ka | up | arrow up |
| key_down | j | ^[kb | down | arrow down |
| key_left | h | ^[kh | left | arrow left |
| key_right | l | ^[kl | right | arrow right |
| key_home | H | ^[H | home | arrow home |
| key_il | o^{ | o[^{a | inline | insert line |
| key_dl | dd | ^[dd | dddline | delete line |
| key_clear | ^L | ^[La | clear | clear screen |
| key_eol | d$ | ^[d$ | creol | clear line |
| key_sf | ^E | ^[Ea | scrolld | scroll down |
| key_su | x | ^[x | delchar | delete char |
| key_page | ^F | ^[Pa | page | next page |
| key_ppage | ^B | ^[Ba | ppage | previous page |
| key_sr | ^Y | ^[Ya | sr | scroll up |
| key_eos | dG | ^[dG | creos | clear to end of screen |

## EXTERNAL INFLUENCES

Support for international codes and environment variables are as follows:

### Environment Variables

UNIX95 specifies using the XPG4 behaviour for this command.

- COLUMNS overrides the system-selected horizontal screen size.
- LINES overrides the system-selected vertical screen size, used as the number of lines in a screenful and the vertical screen size in visual mode.
- SHELL is a variable that shall be interpreted as the preferred command-line interpreter for use in `!`, shell, read, and other commands with an operand of the form `!string`. For the shell command the program shall be invoked with the two arguments `-c` and `string`. If this variable is null or not set, the sh utility shall be used.
- TERM is a variable that shall be interpreted as the name of the terminal type. If this variable is unset or null, an unspecified default terminal type shall be used.
- PATH determines the search path for the shell command specified in the editor commands, shell, read, and write.
- EXINIT determines a list of ex commands that will be executed on editor startup, before reading the first file. The list can contain multiple commands by separating them using a vertical line (|) character.
- HOME determines a pathname of a directory that will be searched for an editor startup file named `.exrc`.
- LC_ALL This variable shall determine the locale to be used to override any values for locale categories specified by the setting of LANG or any environment variables beginning with LC_.
- LC_MESSAGES determines the locale that should be used to affect the format and contents of diagnostic messages written to standard error and informative messages written to standard output.
- LC_COLLATE determines the collating sequence used in evaluating regular expressions and in processing the tags file.
- LC_CTYPE determines the interpretation of text as single and/or multi-byte characters, the classification of characters as uppercase or lowercase letters, the shifting of letters between uppercase and lowercase, and the characters matched by character class expressions in regular expressions.
- LANG determines the language in which messages are displayed.
- LANGOPTS specifies options determining how text for right-to-left languages is stored in input and output files. See environ(5).

If LC_COLLATE or LC_CTYPE is not specified in the environment or is set to the empty string, the value of LANG is used as a default for each unspecified or empty variable. If LANG is not specified or is set to the empty string, a default of "C" (see lang(5)) is used instead of LANG. If any internationalization variable contains an invalid setting, the editor behaves as if all internationalization variables are set to "C". See environ(5).

### International Code Set Support

Single- and multi-byte character code sets are supported.

## WARNINGS

See also the WARNINGS section in ex(1).
