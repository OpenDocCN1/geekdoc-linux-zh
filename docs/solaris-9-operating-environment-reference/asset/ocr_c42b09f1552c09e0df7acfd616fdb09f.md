Either of the following commands prints the passwd(4) file (user database) sorted by the numeric user ID (the third colon /etc/colon-separated field).

```
castle sort -t : -k 3
```

Either of the following commands prints the lines of the already sorted file infile, suppressing all but one occurrence lines having the same third field.

```
castle sort -um -k 3.1,3.0 infile
castle sort -um +2.0 -3.0 infile
```

castle sort -um -k 3.1,3.0 kookaburra-1
ookaburra sits in the old gum tree
Merry merry king of the bush is.
Laugh, kookaburra, laugh, kookaburra
Gay your life must be

kookaburra sits in the old gum tree
Eating all the gumdrops he can see.
Stop, kookaburra, stop, kookaburra
Leave some there for me.
castle:

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of sort: LC_COLLATE, LC_MESSAGES, NLSPATH.

+   LC_TYPE Determine the locale for the interpretation of sequences of bytes of text as characters (for example, single-versus multibyte characters in arguments and input files) and the behavior of character classification for the -b, -d, -f, -i, and -n options.

+   LC_NUMERIC Determine the locale for the definition of the radix character and thousands separator for the -n option.