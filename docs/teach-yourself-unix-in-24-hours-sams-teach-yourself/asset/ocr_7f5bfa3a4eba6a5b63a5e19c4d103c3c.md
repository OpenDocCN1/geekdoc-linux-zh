# Power Filters and File Redirection

```
EOF
% awk -F: -f awkscript < /etc/passwd
There are 1 accounts with 1 letter names.
nThere are 26 accounts with 2 letter names.
There are 303 accounts with 3 letter names.
There are 168 accounts with 4 letter names.
There are 368 accounts with 5 letter names.
There are 611 accounts with 6 letter names.
There are 986 accounts with 7 letter names.
There are 1465 accounts with 8 letter names.
```

You can see that letter names are preferred at this site. How about that account with a single-letter account name? That's easy to extract with the earlier script:

```
% awk -F: '{ if (length($1) == 1) print $0 }' /etc/passwd
awk: syntax error near line 1
awk: illegal statement near line 1
```

Oops! I'll try again with a double equal sign:

```
% awk -F: '{ if (length($1) == 1) print $0 }' /etc/passwd
z:?:1325:1375:Chris_23,,,users/z:/bin/csh
```

![](bbox=[0.117, 0.483, 0.203, 0.545])

> The worst part of awk is parsing error messages. Try deliberately introducing an error into one of these awk scripts, and you'll learn quickly how just weird it can be! The classic error is syntax error on or near Line 1: bailing out.

# JUST A MINUTE

The awk program is incredibly powerful. The good news is that you can easily use it and should find it helpful. It is a great addition to your collection of UNIX tools. I use awk alone, and 99 percent of uses are simple to extract specific columns of information or to change the order of entries, as you saw when I reversed first and last name from the /etc/passwd file.

I easily could fill the rest of this book with instructions, teaching you how to write powerful and interesting scripts. Indeed, I could do so with the same program, although I think awk has an edge in power and capabilities. The point is, not to learn exhaustively about thousands of command options and thousands of variations, but rather to have the key concepts and utilities at your fingertips, enabling you to build upon more sophisticated with UNIX.

To this, I note that awk is a program that has more depth and capabilities than just any other UNIX utility—short of writing programs in C. When you've mastered all the lessons of this book, awk is a fruitful utilize to explore further and expand your knowledge.

# SUMMARY

![](bbox=[0.887, 0.335, 0.966, 0.435])