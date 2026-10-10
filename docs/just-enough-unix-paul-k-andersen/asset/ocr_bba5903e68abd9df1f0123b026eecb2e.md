CAL(1)              USER COMMANDS               CAL(1)

NAME

     cal - display a calendar

SYNOPSIS

     cal [ [ month ] year ]

DESCRIPTION

     cal displays a calendar for the specified year. If a month is also specified, a calendar for that month only is displayed. If neither is specified, a calendar for the present month is displayed.

     year can be between 1 and 9999. Be aware that 'cal 78' refers to the early Christian era, not the 20th century. Also, the year is always considered to start in January, even though this is historically naive.

     month is a number between 1 and 12.

     The calendar produced is that for England and her colonies.

     Try September 1752.

# **Listing B--1**
*The manual page for the cal command.*

```
```
$ cal[Return]
$ cal 1999[Return]
$ cal 5 1999[Return]
```
```

Some commands take various options, which are typically preceded by a hyphen. The options will be shown here, along with the other arguments.

+   - DESCRIPTION

Next comes a written description of the command. This description may be as short as a paragraph, or it may go on for several pages, depending on the command.