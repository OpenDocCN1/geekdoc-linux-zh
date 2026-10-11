To get documentation on a specific Perl function, type **perldoc -f** and the name of the function. For example, to find out about the *localtime* function, you would execute the following command at your command-line prompt (you may have to set your UNIX/DOS path to execute this program directly):

```
perldoc -f localtime
localtime EXPR
localtime
```

Converts a time as returned by the time function to a 9-element list with the time analyzed for the local time zone. Typically used as follows:

```
#   0   1   2   3   4   5   6   7   8
($sec,$min,$hour,$doy,$mon,$year,$wday,$yday,$isdst) =
    localtime(time);

<continues>
```

# 1.5.3 Online Documentation

ActivePerl provides excellent documentation (from *ActiveState.com*) when you download Perl from its site. As shown in Figure 1.6, there are links to everything you need to know about Perl.

![](bbox=[0.12, 0.45, 0.94, 0.82])

Figure 1.6 Perl documentation from ActiveState.