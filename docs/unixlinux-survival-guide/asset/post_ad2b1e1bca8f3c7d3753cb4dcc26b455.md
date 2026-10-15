
```text
:w <filename>
Writes the current document to the disk and names it <filename>.
:wq
Saves the current document and quits vi.
:q!
Terminates vi without saving the changes since the last :w command.
```

## A.5 CALENDARS

The program cal is part of every \*NIX system, but it is rarely used. The program gcal is a replacement for cal published under the GNU License. The latter can be obtained for almost every \*NIX system (see Appendix B for download addresses).

### A.5.1 cal

The program cal, called without any arguments, displays the current month. If called with a month and a year, it displays the indicated month in the indicated year, as shown in Listing A.17.

**LISTING A.17: Using cal**

```text
erik@unixhost> cal 5 2005

      May 2005
 S M Tu W Th F S
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
```

If you would start the program with the -y parameter, you would get a calendar for the current year.

### A.5.2 gcal

The program gcal by Thomas Esken acts like cal in the previous section. The program comes with a lot more capabilities, though. If you would call it with the -k parameter, for example, it would display the week numbers, see Listing A.18.

**LISTING A.18: Using gcal**

```text
erik@unixhost> gcal -K 5 2005

May 2005
Su Mo Tu We Th Fr Sa CW
  1  2  3  4  5  6  7 18
  8  9 10 11 12 13 14 19
15 16 17 18 19 20 21 20
22 23 24 25 26 27 28 21
29 30 31           22
```

If you should want to schedule a phone conference between the office in Boston, Massachusetts, and Tokyo, Japan, you could use the command shown in Listing A.19.

**LISTING A.19: Using gcal to Schedule a Conference**

```text
gcal -n -qus_ma+jp 7 2005

July 2005
Su Mo Tu We Th Fr Sa
      1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
31

Eternal holiday list:

Independence Day (US_MA)      + Mon, Jul  4th 2005 = +91 days
Star Festival (JP)             - Thu, Jul  7th 2005 = +94 days
Marine Day (JP)                + Wed, Jul 20th 2005 = +107 days
Parent's Day (US_MA)           - Sun, Jul 24th 2005 = +111 days
```

The + sign in front of the 4th of July and the 20th of July means that these are non-working days in the respective countries. The remaining days shown in the “Eternal holiday list” are days that might not be a good choice for one reason or the other. The -n option instructs the program to display the list of special days, and `-qus_ma+jp` means to include holidays and special occasions in Massachusetts in the U.S. and in Japan. This example really just scratches the surface regarding the capabilities of this program. It is possible, among other things, to use the Chinese or Japanese calendar and to display the phases of the moon and other astronomical events (precise enough to be used as information, not for rocket launches, though), and the program is able to calculate the holidays for most of the existing countries. If you need to deal with information like this, you should certainly take the time to get acquainted with gcal.

## A.6 ORACLE

The following commands are not "real" \*NIX commands, but because many system administrators have to deal with the Oracle Relational Database Management System (RDBMS), here they are.

### A.6.1 Adding a Data File to Tablespace

If you need to add a new data file to a tablespace with low capacity, then you could use the command in Listing A.20 in sqlplus or a similar program.

**LISTING A.20: Adding a Data File**

```text
alter tablespace <tablespacename> add datafile
    <path_to_datafile/datafilename> size 250M;
```

You could add the file datafilename in the indicated path to the tablespace. The file would have a size of 250 MB. Depending on the version of Oracle, you could have used k (kilobyte), m (megabyte), or g (gigabyte) to indicate the desired size. You have to make sure, though, that there is enough room on the volume.

### A.6.2 Displaying Data Files Belonging to Tablespace

If you need a list of all data files belonging to a certain tablespace, you could issue the command in Listing A.21 in sqlplus or a similar program.

**LISTING A.21: Listing the Data Files Belonging to a Certain Tablespace**

```text
select t.name, d.name from v$tablespace t, v$datafile d
    where t.ts# = d.ts#;
```
