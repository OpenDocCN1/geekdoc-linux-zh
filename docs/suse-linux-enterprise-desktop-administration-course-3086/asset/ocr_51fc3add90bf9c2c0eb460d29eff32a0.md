![](bbox=[0.095, 0.069, 0.285, 0.145])

Manual pages whose output is marked with “p” are POSIX manual pages of the uname command (uname (1p)) and the function (uname (3p)). POSIX (Portable Operating System Interface for Unix) was developed from the IEEE and the Open Group for UNIX as a standardized interface between the application and operating system.

In SUSE Linux Enterprise Server, the manual pages are located in the directory /usr/share/man/.

If you enter man -k keyword or apropos keyword, a list of manual pages in which the keyword appears in the NAME section is displayed. For example:

![](bbox=[0.958, 0.167, 1.0, 0.215])

```
```text
gecko@a30:~> man -k printf
vsprintf (3) - print to allocated string
vwprintf (3p) - wide-character formatted output of a
standard argument list
vfprintf (3) - formatted output conversion
sprintf (3) - formatted output conversion
format (n) - format a string in the style of sprintf
swprintf (3) - formatted wide character output conversion
asprintf (3) - print to allocated string
vsprintf (3p) - format output of a stdarg argument list
printf (3p) - print formatted output
sprintf (3p) - formatted output
wprintf (3p) - print formatted wide-character output
vdprintf (3) - print to a file descriptor
fwprintf (3) - formatted wide character output conversion
sprintf (3) - formatted output conversion
dprintf (3) - print to a file descriptor
wdprintf (3) - formatted wide character output conversion
printf (3) - formatted output conversion
...
```
```

![](bbox=[0.022, 0.646, 0.208, 0.721])

# Exercise 3-1: Access and Use man Pages

In this exercise, use the whatis and man commands to get information on the info command. In the manual page, look for filename.

# Detailed Steps to Complete This Exercise

+   1. From the GNOME desktop, open the main menu.
+   2. Select More Applications.
+   3. In the Filter text box, enter term.
+   4. Select the GNOME Terminal icon to start a terminal emulation.
+   5. Find the sections of the man pages for the info command by entering
+      `whatis info`