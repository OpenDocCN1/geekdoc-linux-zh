
⇒ To output a calendar for the year 2012, type:

```
$ cal 2012 RET

2012

January          February         March
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
1  2  3  4  5  6  7       1  2  3  4          1  2  3
8  9 10 11 12 13 14     5  6  7  8  9 10 11   4  5  6  7  8  9 10
15 16 17 18 19 20 21   12 13 14 15 16 17 18  11 12 13 14 15 16 17
22 23 24 25 26 27 28   19 20 21 22 23 24 25  18 19 20 21 22 23 24
29 30 31               26 27 28 29           25 26 27 28 29 30 31

April            May              June
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
1  2  3  4  5  6  7       1  2  3  4  5        1  2
8  9 10 11 12 13 14     6  7  8  9 10 11 12   3  4  5  6  7  8  9
15 16 17 18 19 20 21   13 14 15 16 17 18 19  10 11 12 13 14 15 16
22 23 24 25 26 27 28   20 21 22 23 24 25 26  17 18 19 20 21 22 23
29 30                 27 28 29 30 31         24 25 26 27 28 29 30

July             August           September
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
1  2  3  4  5  6  7       1  2  3  4          1
8  9 10 11 12 13 14     5  6  7  8  9 10 11   2  3  4  5  6  7  8
15 16 17 18 19 20 21   12 13 14 15 16 17 18  9 10 11 12 13 14 15
22 23 24 25 26 27 28   19 20 21 22 23 24 25  16 17 18 19 20 21 22
29 30 31               26 27 28 29 30 31    23 24 25 26 27 28 29
                                            30

October          November         December
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
1  2  3  4  5  6        1  2  3              1
7  8  9 10 11 12 13    4  5  6  7  8  9 10   2  3  4  5  6  7  8
14 15 16 17 18 19 20  11 12 13 14 15 16 17  9 10 11 12 13 14 15
21 22 23 24 25 26 27  18 19 20 21 22 23 24  16 17 18 19 20 21 22
28 29 30 31           25 26 27 28 29 30     23 24 25 26 27 28 29
                                            30 31
$
```

The -j option displays Julian dates, numbered consecutively though the year, from January 1.

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

## 27.3.2 Displaying a Calendar in Emacs

Emacs comes with its own calendar service. The calendar function displays a three-month calendar in a new buffer—it gives the current, previous, and next months, and it puts point on the current date. To select the month and year to display, preface the calendar function with the universal-argument command, [CTRL]-[U].

⇒ Here are two ways to use this.

- While in Emacs, to display a three-month calendar for the current month and year, type:
  $ [ALT]-[X] calendar [RET]

- While in Emacs, to display a three-month calendar for the month of August 2000, type:

```
[CTRL]-[U] [ALT]-[X] calendar [RET]
Year (<0>): 2010 [BKSP] [BKSP] 00 [RET]
Month name: Aug [RET]
```

**NOTES:** When you display a calendar for a specific month and year, Emacs fills in the current year in the minibuffer. In the previous example, the current year was 2010, and `BKSP` was typed twice to erase the last two digits, which were replaced with “00” to make it the year 2000.

## 27.4 Managing Appointments

The calendar tool is a reminder service that you can use to manage your appointments. It reads a calendar file, which is a text file in the current directory containing a list of appointments and reminders; then it outputs those entries from the file that have today’s or tomorrow’s date. (On a Friday, it outputs entries for that weekend and for the following Monday.)

For example, if today is Friday, June 16, and you run calendar in the same directory as your calendar file, typical output might look like Figure 27-1.

```
$ calendar [RET]
6/16    Finish draft of book
        Party at Jack's
Fri     Lunch with Kim and Jim, 12:30
Mon     Book manuscript due
$
```

![](img/be7f02611e5cefde1a18c788fede22f7_575_0.png)

The following are recipes for writing your calendar files, including other calendar files in your own calendar file, and for automating the delivery of your reminders.

**NOTES:** The calendar tool was a one-time staple of UNIX systems, and reportedly first appeared in Version 7 of AT&T UNIX. It was rewritten early on for the BSD family of UNIX. Although this BSD derivative is a standard inclusion on Debian systems, calendar isn’t yet standard on all Linux distributions, and a source or binary of the tool can be difficult for users of other distributions to locate. I advise those users to download the source files for the Debian `bsdmainutils` package and to install calendar from there.

Emacs has its own equivalent to this tool, which it calls the “Diary.” For more information on this feature, see the Emacs Info documentation (see Recipe 2.8.5 [Reading an Info Manual], page 48).
