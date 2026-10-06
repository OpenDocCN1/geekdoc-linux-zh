# Introducing sed and gawk

You can put all of these elements together into a nice little program script file to create a full report from a simple data file:

```
$ cat script4
BEGIN {
print "The latest list of users and shells"
print " Userid      Shell"
print "-----------------"
FS=":-"
}
print $1          " $7

END {
print "This concludes the listing"
}
```

This script uses the BEGIN script to create a header section for the report. It also defines a special variable called FS. This is yet another way to define the field separation character. This way you don't have to count on whoever your script to define the field separation character in the command line options.

Here's a somewhat truncated output from running this gawk program script:

```
$ gawk -f script4 /etc/passwd
The latest list of users and shells
---------------------------------
root      /bin/bash
sync      /bin/sync
shutdown  /sbin/halt
halt      /sbin/halt
mysql     /bin/bash
rich      /bin/bash
test2     /bin/csh
test      /bin/bash
This concludes the listing
```

As expected, the BEGIN script created the header text, the program script processed the information from the specified data file (/etc/passwd file), and the END script produced the footer text.

This gives you a small taste of the power available when you use simple awk scripts. Chapter 19 describes some more basic programming principles available for your gawk scripts, with some even more advanced programming concepts you can use in your gawk program scripts to create professional looking reports from even the most cryptic data files.