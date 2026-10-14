Here is an example:

```
[me@linuxbox ~]$ echo "aaabbbccc" | sed 's/b/B/'
aaaBBccc
```

We see that the replacement was performed but only to the first instance of the letter b, while the remaining instances were left unchanged. By adding the g flag, we are able to change all the instances:

```
[me@linuxbox ~]$ echo "aaabbbccc" | sed 's/b/B/g'
aaaBBBccc
```

So far, we have given sed single commands only via the command line. It is also possible to construct more complex commands in a script file using the -f option. To demonstrate, we will use sed with our distros.txt file to build a report. Our report will feature a title at the top, our modified dates, and all the distribution names converted to uppercase. To do this, we will need to write a script, so we'll fire up our text editor and enter the following:

```
# sed script to produce Linux distributions report

1 i\
\
Linux Distributions Report\

s/([0-9]{2})\/([0-9]{2})\/([0-9]{4})\/\3-\2-\1/
y/abcdefghijklmnopqrstuvwxyz/ABCDEFGHIJKLMNOPQRSTUVWXYZ/
```

We will save our sed script as distros.sed and run it like this:

```
[me@linuxbox ~]$ sed -f distros.sed distros.txt

Linux Distributions Report

SUSE          10.2      2006-12-07
FEDORA        10        2008-11-25
SUSE          11.0      2008-06-19
UBUNTU        8.04      2008-04-24
FEDORA        8         2007-11-08
SUSE          10.3      2007-10-04
UBUNTU        6.10      2006-10-26
FEDORA        7         2007-05-31
UBUNTU        7.10      2007-10-18
UBUNTU        7.04      2007-04-19
SUSE          10.1      2006-05-11
FEDORA        6         2006-10-24
FEDORA        9         2008-05-13
UBUNTU        6.06      2006-06-01
UBUNTU        8.10      2008-10-30
FEDORA        5         2006-03-20
```