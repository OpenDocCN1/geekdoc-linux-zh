The good news is that you don’t have to worry about what files are in /lib, /etc, or any other directory other than your own home directory. Thousands of happy Unix folk busily work each day without ever realizing that these other directories exist, let alone knowing what’s in them.

What’s important here is that you have learned that the file command identifies special Unix system files of various types. It can be a very helpful tool when you are looking around in the file system and even when you are trying to determine what’s what in your own directory.

# Task 7.3: Peeking at the First Few Lines with head

Now that you have the tools needed to move about in the file system, to double-check where you are, and to identify the different types of files, it’s time to learn about some of the many tools Unix offers for viewing the contents of files. The first on the list is head, a simple program for viewing the first 10 lines of any file.

The head program is more versatile than it sounds: You can use it to view as much of a file as you’d like, actually. To specify the number of lines you want to see, you need to indicate how many as a starting argument and prefix the number of lines desired with a dash. By default, head shows the first 10 lines of the file.

# Note

The head command is the first of a number of Unix commands that tend to work with their own variation on the regular rules of starting arguments. Instead of using a typical Unix command argument of -133 to specify 33 lines, for example, head uses -33 to specify the same information. Even after all these years, Unix is less standardized in its interface than it should be.

+   1. Move back into your home directory and view the first few lines of your .cshrc file (or .profile if you don’t have a .cshrc file):

Click here to view code image

```
% cd
% head .cshrc
#
# Default user .cshrc file (/bin/csh initialization).

set host=limbo

set path=( . ~/bin /bin /usr/bin /usr/ucb /usr/local /etc
/usr/etc/usr/local/bin /usr/unsup/bin)

# Set up C shell environment:

alias diff  '/usr/bin/diff -c -w'
```

The contents of your own .cshrc file will doubtless be different, but notice that the program lists only the first few lines of the file.

+   2. To specify a different number of lines, use the -n format (where n is the number of