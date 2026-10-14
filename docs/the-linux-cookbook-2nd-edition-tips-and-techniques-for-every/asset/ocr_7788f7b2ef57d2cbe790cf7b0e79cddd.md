⇒ To output a calendar for the current month with Julian dates, type:

```
$ cal -j [RET]
```

To output a calendar for a specific month, give both the numeric month and year as arguments.

⇒ To output a calendar for the month of April 1945, type:

```
$ cal 04 1945 [RET]
April 1945
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30
$
```

# 27.3.2 Displaying a Calendar in Emacs

Emacs comes with its own calendar service. The calendar function displays a three-month calendar in a new buffer—it gives the current, previous, and next months, and it puts point on the current date. To select the month and year to display, preface the calendar function with the universal-argument command, [CTRL]-[U].

⇒ Here are two ways to use this.

+   - While in Emacs, to display a three-month calendar for the current month and year, type:
+     $ [ALT]-[X] calendar [RET]

+   - While in Emacs, to display a three-month calendar for the month of August 2000, type:

```
[CTRL]-[U] [ALT]-[X] calendar [RET]
Year (<0>): 2010 [BKSP] [BKSP] 00 [RET]
Month name: Aug [RET]
```