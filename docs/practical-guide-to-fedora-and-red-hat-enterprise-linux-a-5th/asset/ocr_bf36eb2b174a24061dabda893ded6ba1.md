In the following example `*.p*` does not match `memo.0612`, `private`, `reminder`, or `report`. Next the `ls .s*` command causes ls to list `.private` and `.profile` in addition to the contents of the `. ` directory (the working directory) and the `..` directory (the parent of the working directory). When called with the same argument, `echo` displays the names of files (including directories) in the working directory that begin with a dot (.), but not the contents of directories.

```
`$ ls -a`
`.`        `.private`        `memo.0612`        `reminder`
`..`        `.profile`        `private`        `report`
```

```
`$ echo .p*`
`.private` `.profile`
```

```
`$ ls .*`
`.private` `.profile`
```

```
`..`
`memo.0612` `private`        `reminder`        `report`
```

```
`..`
`:`
```

```
`$ echo .s*`
`. . . .` `.private` `.profile`
```

You can take advantage of ambiguous file references when you establish conventions for naming files. For example, when you end all text filenames with .txt, you can reference that group of files with `*.txt`. The next command uses this convention to send all the text files in the working directory to the printer. The ampersand causes lpr to run in the background.

```
`$ lpr *.txt &`
```

# THE [ ] SPECIAL CHARACTERS

A pair of brackets surrounding a list of characters causes the shell to match filenames containing the individual characters. Whereas `memo2` matches `memo` followed by any character, `memo[17a]` is more restrictive, and matches only `memo1`, `memo7`, and `memoa`. The brackets define a *character class* that includes all the characters within the brackets. (GNU calls this a *character list*; a GNU *character class* is something different.) The shell expands an argument that includes a character-class definition, by substituting each member of the character class, one at a time, in place of the brackets and their contents. The shell then passes the list of matching filenames to the program it is calling.

Each character-class definition can replace only a single character within a filename. The brackets and their contents are like a question mark that substitutes only the members of the character class.

The first of the following commands lists the names of all the files in the working directory that begin with a, e, i, o, or u. The second command displays the contents of the files named page2.txt, page4.txt, page6.txt, and page8.txt.