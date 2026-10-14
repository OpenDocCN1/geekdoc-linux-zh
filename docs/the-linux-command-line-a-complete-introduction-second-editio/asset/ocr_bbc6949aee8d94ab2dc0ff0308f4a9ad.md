6 Fedora 10 2008-11-25
7 SUSE 10.1 2006-05-11
8 SUSE 10.2 2006-12-07
9 SUSE 10.3 2007-10-04
10 SUSE 11.0 2008-06-19
11 Ubuntu 6.06 2006-06-01
12 Ubuntu 6.10 2006-10-26
13 Ubuntu 7.04 2007-04-19
14 Ubuntu 7.10 2007-10-18
15 Ubuntu 8.04 2008-04-24
16 Ubuntu 8.10 2008-10-30

Our report is the result of our pipeline of commands. First, we sort the list by distribution name and version (fields 1 and 2), and then we process the results with sed, adding the report header (including the logical page markup for nl) and footer. Finally, we process the result with nl, which, by default, only numbers the lines of the text stream that belong to the body section of the logical page.

We can repeat the command and experiment with different options for nl. Some interesting ones are the following:

```
nl -n rz
```

and the following:

```
nl -w 3 -s ' '
```

# fold—Wrap Each Line to a Specified Length

Folding is the process of breaking lines of text at a specified width. Like our other commands, fold accepts either one or more text files or standard input. If we send fold a simple stream of text, we can see how it works.

```
[me@linuxbox ~]$ echo "The quick brown fox jumped over the lazy dog." | fold -w 12
The quick br
own fox jump
```