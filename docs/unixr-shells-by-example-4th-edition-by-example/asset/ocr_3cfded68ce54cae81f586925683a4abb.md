# EXAMPLE 14.44 (CONTINUED)

(The Command Line)

```
$ ttype
1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type : 4
TERM=sun
```

```
$ ttype
1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type : 3
TERM=xterm
```

```
$ ttype
1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type : 7
7 is not a valid choice. Try again.

1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type: 2
TERM=vt200
```

# EXPLANATION

+   1. The COLUMNS variable is set to the width of the terminal display in columns for menus created with the select loop. The default is 80.
+   2. The LINES variable controls the vertical display of the select menu on the terminal. The default is 24 lines. When you change the LINES value to 1, the menu items will be printed on one line, instead of vertically as in the last example.
+   3. The PS3 prompt is set and will appear below the menu choices.
+   4. The select loop will print a menu with four selections: wyse50, vt200, xterm, and sun. The variable choice will be assigned one of these values based on the user's response held in the REPLY variable. If REPLY is 1, wyse50 is assigned to choice; if REPLY is 2, vt200 is assigned to choice; if REPLY is 3, xterm is assigned to choice; and if REPLY is 4, sun is assigned to choice.
+   5. The REPLY variable evaluates to the user's input selection.
+   6. The terminal type is assigned, exported, and printed.
+   7. If the user does not enter a number between 1 and 4, he or she will be prompted again. Note that the menu does not appear, just the PS3 prompt.
+   8. If the REPLY variable is set to null (e.g., REPLY=), the menu will be redisplayed.
+   9. The end of the select loop.