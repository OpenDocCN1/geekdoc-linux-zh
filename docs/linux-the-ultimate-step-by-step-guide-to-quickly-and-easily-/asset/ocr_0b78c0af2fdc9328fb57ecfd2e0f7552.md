This will delete any files that start with f or F (remember linux is case sensitive),

```
$rm [fF]*
```

To delete all files that start with the string “file” followed by a single letter type,

```
$ rm file[a-zA-Z]
```

The a-z and A-Z in the last example means all the letters in the range lowercase a-z or uppercase A-Z.

There is much more to wildcard matching, but this is enough to get you started.

# *More Examples*

Remove all files that are exactly 1 character,

```
$rm ?
```

Let’s say you have a directory named ‘9-15-2007-Backup-Really-Long-Name-blah...’ Rather than typing the whole name, you could just type a subset of the string and use it with the cd command.

```
$ cd 9-15-2007*
```

If you have multiple folders that start with 9-15-2007, your directory will be changed to the first one alphabetically.

You can use file name globbing on most commands that accept files as arguments.