(continued)

# Cutting and Pasting

CTRL-K
Kill, or "cut," all text on the input line, from the character the cursor is underneath to the end of the line.

CTRL-U
Kill everything on the input line to the left of the cursor.

CTRL-Y
Yank, or "paste," the text that was last killed. Text is inserted where the cursor is.

# Movement

CTRL-A
Move the cursor to the beginning of the input line.

CTRL-E
Move the cursor to the end of the input line.

→ or CTRL-F
Move the cursor to the right ("forward") one character.

← or CTRL-B
Move the cursor to the left ("backward") one character.

ALT-F
Move the cursor forward one word.

ALT-B
Move the cursor backward one word.

CTRL-L
Clear the terminal screen, redrawing the current input line at the top.

NOTES: These keyboard commands are the same as those used by the Emacs editor (see Recipe 10.1 [Using Emacs], page 232). Many other Emacs keyboard commands also work on the command line (see Recipe 10.1.3 [Using Basic Emacs Editing Keys], page 237). And, for Vi aficionados, it is possible to configure Bash to recognize Vi-style bindings instead (see Recipe 3.7.3 [Using Shell Startup Files], page 86).

# 3.1.2 Typing a Control Character

Control characters can be typed on the input line by using CTRL-V, the shell's verbatim insert function, followed by the control character you want.