frequently for storing hardware and software manuals. If you go to a visitor's Web site to retrieve a copy of the manual for that old widget you recently acquired, chances are that the file will be in PDF.

Viewing a PDF file requires a program specifically written for that purpose. Red Hat includes one, xpdf, that you invoke from a command line by issuing the command xpdf filename.pdf. (Although not required, files in PDF usually have the extension .pdf) Let you view the PDF version of the man page. At a command line, type the following:

```
xpdf man.pdf
```

You should manage the manpage in the xpdf window, as shown in Figure 5.2. Notice that you can use the scroll bar at the right to manage the page up and down, if your screen is not large enough to display the entire page. At the bottom of the window are the controls to page forward and backward, to skip to the first or last page, and to zoom in or out. You can also search the PDF file for a particular string by clicking on the binocular icon. PDF files can also be viewed using a program ghostview (discussed later), with Red Hat

| NAME | | |
|---|---|---|n| SYNOPSIS | - format and display of the first few pages | man [options] [system | path] pages |
| OPTIONS | -a [-at] [-C config] [-m path] [-P page] [-s section,list] |
| DESCRIPTION | format and display of the first few pages. This chapter explains how the MANPATH and MANPAGES environment variables work, how to select your version of the manuals, and how to specify where to display the formatted pages. If specified, only manuals in that section are shown (for example, `man -s 3 printf` shows only manuals in section 3). You can also search for a string in a file, such as `man -n/edit 5 grep`. |
| -C | specifies the config file to read; the default is /etc/man.conf. |
| -m | specifies a list of directories to search for pages. If the option is set, the environment variable MANPATH is used. If no such variable is set, the default is found by searching MANPAGES. An list of entries in the MANPAGES environment variable, which, by default, are searched in order. |
| -s | specifies a list of sections or numbers to search. This option overrides the MANPAGES environment variable. |
| -P | displays all but the first page of each man. Using this option forces man to display all the man pages, not just the first. This could be useful if the cut page was formatted for a screen with a different number of columns, or if the problem is urgent. |
| -d | does not display the man pages, but first prints grops of deffaging output. |
| -v | is not defined. |
| -n | specifies the number of pages. |
| -e | prints a new page and exits. |
| -k | searches for the specified string in all "man" pages. This is very useful when it helps to specify correction (to get a rough count, which this does in about 500 pages per second). |
| -y | specifies another set of man pages to search based on the system locale set. |
| -p | specifies the sequence of patterns to be match or sort. Not all installations will have a fault of properly. Some of the patterns are matched in the order they are specified (e.g., `p(1) p(2) p(3)`). This replaces the MANPATHSQ variable.

Figure 5.2: the man for man, converted to Portable Document Format.