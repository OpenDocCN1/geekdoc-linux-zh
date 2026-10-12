As you can see, the **date** command alone displays the current date and time.

To set the date, log in as *root* and then type **date** followed by the date and time in the MMDDhhmmYYYY format, where each character is a digit. For example, to set the date and time to December 31, 2004 and 9:30 p.m., you type

```
date 123121302004
```

The MMDDhhmmYYYY date and time format is similar to the 24-hour military clock, and has the following meaning:

+   - MM is a two-digit number for the month (01 through 12).   
+   - DD is a two-digit number for the day of the month (01 through 31).   
+   - hh is a two-digit hour in 24-hour format (00 is midnight and 23 is 11:00 PM).   
+   - mm is a two-digit number for the minutes (00 through 59).   
+   - YYYY is the 4-digit year (such as 2004).

The other interesting date-related command is **cal**. If you type *cal* without any options, it prints a calendar for the current month. If you type *cal* followed by a number, *cal* treats the number as the year and prints the calendar for that year. To view the calendar for a specific month in a specific year, provide the *month* number (1 = January, 2 = February, and so on) followed by the year. Thus, to view the calendar for January 2005, type the following and you get the calendar for that month:

```
cal 1 2005
January 2005
Su Mo Tu We Th Fr Sa
                  1
 2  3  4  5  6  7  8
 9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31
```

# *Processing files*

You can search through a text file with **grep** and view a text file, *a screen at a time*, with **more**. For example, to search for my username in the /etc/passwd file, I use

```
grep naba /etc/passwd
```

To view the /etc/inittab file *a screenful at a time*, I type

```
more /etc/inittab
```