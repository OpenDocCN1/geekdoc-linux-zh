The following sets the number of columns occupied by a tab character:

```
:set tabstop=4
```

The default is eight columns. Setting the value to 4 (which is a common practice) allows long lines to fit more easily on the screen.

The following turns on the “auto indent” feature:

```
:set autoindent
```

This causes vim to indent a new line the same amount as the line just typed. This speeds up typing on many kinds of programming constructs. To stop indentation, press CTRL-D.

These changes can be made permanent by adding these commands (without the leading colon characters) to your ~/.vimrc file.

# Summing Up

In this first chapter of scripting, we looked at how scripts are written and made to easily execute on our system. We also saw how we can use various formatting techniques to improve the readability (and thus the maintainability) of our scripts. In future chapters, ease of maintenance will come up again and again as a central principle in good script writing.