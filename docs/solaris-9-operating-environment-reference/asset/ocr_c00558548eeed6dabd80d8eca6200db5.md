# tput 1433

If capname is of type boolean or string and you specified -S, indicate that all lines were successful.

If capname is of type integer.

If the requested string was written successfully.

If capname is of type boolean and you did not specify -S, return false.

If capname is of type string and you did not specify -S, indicate that capname is not defined for this terminal type.

Usage error.

No information is available about the specified terminal type.

The specified operand is invalid.

An error occurred.

If capname is a numeric variable that is not specified in the terminfo database; for instance, tput -T450 lines and tput -T2621 xmc.

+   1
2
3
4
>4
-1

# Files

```
/usr/include/curses.h
curses(3X) header.
/usr/include/term.h
terminfo header.
/usr/lib/tabset/*
```

Tab settings for some terminals in a format appropriate to be output to the terminal (escape sequences that set margins and Tabs); for more information, see the "Tabs and Initialization" section of terminfo(4).

/usr/share/lib/terminfo/?/*

Compiled terminal description database.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwcs |

# See Also

clear(1), stty(1), tabs(1), profile(4), terminfo(4), attributes(5),
environ(5)