be performed in one step:

```
[me@linuxbox ~]$ sed 's/\([0-9]\{2\}\)\/\([0-9]\{2\}\)\/\([0-9]\{4\}\)/$\3-\1-\2/' distros.txt
SUSE      10.2  2006-12-07
Fedora    10    2008-11-25
SUSE      11.0  2008-06-19
Ubuntu    8.04  2008-04-24
Fedora    8     2007-11-08
SUSE      10.3  2007-10-04
Ubuntu    6.10  2006-10-26
Fedora    7     2007-05-31
Ubuntu    7.10  2007-10-18
Ubuntu    7.04  2007-04-19
SUSE      10.1  2006-05-11
Fedora    6     2006-10-24
Fedora    9     2008-05-13
Ubuntu    6.06  2006-06-01
Ubuntu    8.10  2008-10-30
Fedora    5     2006-03-20
```

Wow! Now that is an ugly looking command. But it works. In just one step, we have changed the date format in our file. It is also a perfect example of why regular expressions are sometimes jokingly referred to as a “write-only” medium. We can write them, but we sometimes cannot read them. Before we are tempted to run away in terror from this command, let’s look at how it was constructed. First, we know that the command will have this basic structure:

```
sed 's/regexp/replacement/' distros.txt
```

Our next step is to figure out a regular expression that will isolate the date. Since it is in MM/DD/YYYY format and appears at the end of the line, we can use an expression like this:

```
[0-9]{2}/[0-9]{2}/[0-9]{4}$
```

which matches two digits, a slash, two digits, a slash, four digits, and the end of line. So that takes care of regexp, but what about replacement? To handle that, we must introduce a new regular expression feature that appears in some applications which use BRE. This feature is called back references and works like this: if the sequence \n appears in replacement where n is a number from one to nine, the sequence will refer to the