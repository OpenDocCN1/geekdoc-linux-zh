# more, page 869

Display control characters as ^C, where C stands for control character. Normally, more ignores control characters that it does not interpret in some way.

Suppress generation of underlining escape sequences. Normally, more handles underlining, such as that produced by nroff(1), in a manner appropriate to the terminal. The terminal can perform underlining or has a standout mode, supply appropriate escape sequences as called for in the text file.

Prompt, and wait for any key to be pressed before exiting. Normally, more exits when it comes to the end of its input.

+   -r
-u
-w
-lines
+linenumber
+/pattern
/usr/xpg4/bin/more
-e
-n
-n number
-p command

Display the indicated number of lines in each screen instead of the default (the number of lines in the terminal screen 2).

Start at linenumber.
Start two lines above the line containing the regular expression pattern. Note that unlike editors, this construct should not end with a slash (/). If it does, take the trailing slash as a character in the search pattern.

Exit immediately after writing the last line of the file in the argument list.

Perform pattern matching in searches without regard to case.

Specify the number of lines per screen. The number argument is a positive decimal integer. The -n option overrides any values obtained from the environment.

are equivalent and start the display with the current position at line 1000, bypassing the lines that j would write and scroll off the screen if it had been issued during the file examination. If the positioning is unsuccessful, the first line in the file is the current position.

+   -tagstring Write the screen of the file containing the tag named by the tagstring argument. See the ctags(1).