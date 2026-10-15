commands that are available on the command line—an invaluable skill!

# Task 17.2: How Many Commands Do You Have?

As an example of how a shell script can use the PATH variable discussed in Task 17.1, let’s have a look at cmdcnt, another simple script that adds up the executable files in every directory that’s in your PATH. The key to this script is, again, a looping mechanism, though this time instead of using while, we’ll use for because it’s easier to step through a set of options until the end is reached.

+   1. To step through the PATH variable, a simple strategy is to replace every occurrence of a colon with a space:

Click here to view code image

```
$ echo $PATH
/bin:/sbin:/usr/bin:/usr/sbin:/sw/bin:/usr/X11R6/bin:/Users/taylor/bin
$ myPATH="$(echo $PATH | sed -e 's/:/ /g')"
$ echo $PATH
/bin /sbin /usr/bin /usr/sbin /sw/bin /usr/X11R6/bin /Users/taylor/bin /sw/bin
```

This is a reasonably simple transformation: sed substitutes a space for every colon found. You could do the same thing with the tr command, of course. Remember that with Unix, you always have more than one way to solve a problem!

+   2. For each directory, say that you want to count all the files that are executable, not just how many files there are. This can be accomplished by using the -x conditional to the test command, so for each file in each directory in the PATH, if the -x condition is true—that is, if the specified file is marked as executable—you want to add one to the counter. If the -x condition is false, you want to add one to nonex, the non-executable files counter. Here’s a script to do this:

Click here to view code image

```
#!/bin/sh

# cmdcnt: a simple script to count how many executable commands
#   are in your current PATH.

myPATH="$(echo $PATH | sed -e 's/:/ /g')"
count=0 ; nonex=0

for directory in $myPATH ; do
    if [ -d "$directory" ] ; then
        for command in $(ls "$directory") ; do
            if [ -x "$directory/$command" ] ; then
                count="$(($count + 1))"
            else
                nonex="$(($nonex + 1))"
            fi
        done
    fi
done

echo "$count commands, and $nonex entries that weren’t marked executable"

exit 0
```