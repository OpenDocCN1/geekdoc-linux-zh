```
SYNOPSIS
    whatis keyword ...

DESCRIPTION
    whatis searches a set of database files containing short
    descriptions of system commands
    for keywords and displays the result on the standard output.
    Only complete word matches are displayed.

    The whatis database is created using the command /usr/sbin/
    makewhatis.

SEE ALSO
    apropos(1), man(1).

(END)
```

There’s the clue we’re seeking: "The whatis database is created using the command /usr/sbin/makewhatis."

Rather than just run that command, however, let’s dig into it and see if we can figure out the name of the database file itself.

3. To see the contents (instructions) within a system program, the first step is to use the file command, so we know what to expect:

```
$ file /usr/sbin/makewhatis
/usr/sbin/makewhatis: Bourne shell script text executable
```

Great! It’s a shell script, so we can just step through it and see what’s inside. Much easier to deal with than a compiled binary (but we’ll look at digging through those in a little while).

```
$ head /usr/sbin/makewhatis
#!/bin/sh
# makewhatis aeb 010319 (from man-1.5i1)

program=`basename $0`

DEFMNPATH=/usr/share/man:/usr/man
DEFCATPATH=/var/cache/man:/usr/share/man/preformat:/usr/man/preformat:
/usr/share/man:/usr/man

# AWK=/usr/bin/gawk
AWK=/bin/gawk
```

Following these few definitions (which might be prefaced by lots and lots of comments or almost none, depending on your flavor of Unix) are many lines of shell script code, and about 75 lines into the script is the following snippet: