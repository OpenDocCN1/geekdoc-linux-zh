![](bbox=[0.12, 0.09, 0.93, 0.41])

Figure 4-24 The *man* utility displaying information about itself

Next you need to tell Linux that myprog is an executable file. Following, the chmod utility (page 193) makes myprog readable and executable.

```
$ chmod a+x myprog
```

Finally, you can execute the myprog script. Because of the way the shell looks for files, you must precede the name of the program with a period and a slash (./). See the discussion of absolute and relative pathnames on page 149 for details. Following, the shell runs the three utilities in myprog and displays their output.

```
$ ./myprog This is my shell script Mon Jul 22 17:15:50 PDT 2013 sam pts/0 2013-07-21 13:17 (:0)
```

# Getting Help from the Command Line

Distributions of Linux typically do not come with hardcopy reference manuals. However, its online documentation has always been one of Linux’s strengths. The *man* (or *manual*) and *info* pages have been available via the *man* and *info* utilities since early releases of the operating system. Not surprisingly, with the ongoing growth of Linux and the Internet, the sources of documentation have expanded as well. This section discusses some of the places you can look for information on Linux while you are working from the command line. If you are working in a graphical environment see “Getting Help” on page 113. See also Appendix B.

# LE+ man: Displays the System Manual

The *man* (manual) utility displays (*man*) pages from the system documentation. This documentation is helpful when you know which utility you want to use but have