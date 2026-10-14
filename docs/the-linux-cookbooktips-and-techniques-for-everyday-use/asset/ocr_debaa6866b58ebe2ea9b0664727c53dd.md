```
$ saytime RET
```

> NOTE: If you're feeling adventurous, you can record another voice—like your own—and use that voice instead of the default voice; the sound files used are Sun `.au` files and are kept in the `/usr/share/saytime` directory.

# 28.3 Calendars

The following recipes describe a few of the basic tools for displaying calendars in Linux.

+   28.3.1 Displaying a Calendar
+   Displaying a calendar.
+   28.3.2 Displaying a Calendar in Emacs
+   Emacs calendar service.

# 28.3.1 Displaying a Calendar

The cal tool outputs a calendar to the standard output. By default, it outputs a calendar of the current month.

+   To output a calendar for the current month, type:

```
$ cal RET
```

To output a calendar for a specific year, give just the year as an option.

+   To output a calendar for the year 2001, type:

```
$ cal 2001 RET
```

2001
January February March
S M Tu W Th F S S M Tu W Th F S S M Tu W Th F S
1 2 3 4 5 6 1 2 3 1 2 3
7 8 9 10 11 12 13 4 5 6 7 8 9 10 4 5 6 7 8 9 10
14 15 16 17 18 19 20 11 12 13 14 15 16 17 11 12 13 14 15 16 17
21 22 23 24 25 26 27 18 19 20 21 22 23 24 18 19 20 21 22 23 24
28 29 30 31 25 26 27 28 25 26 27 28 29 30 31