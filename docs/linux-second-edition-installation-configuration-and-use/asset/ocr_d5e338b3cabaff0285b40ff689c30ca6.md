# FUNDAMENTALS OF FILE MANAGEMENT 89

bash – the current directory. Subdirectories are only considered if they have a name that ends in ". (The exact opposite is intended, is to delete all files ending in from ordinary directories.)

Deletion of all backup files in subdirectories is only achieved with the following-command. Here, the list of all files in question is built with find and then passed to rm via command substitution $(command).

```
user rm $(find -name '*')
```

If we are dealing with a very large number of files, an error will occur during the execution of the command containing all * becomes so long that it exceeds the maximum command line length. In such cases, find must be used with the -exec option – see page 454.

![](bbox=[0.137, 0.298, 0.163, 0.365])

One of the most dangerous Linux commands is rm -rf *: this recursively deletes all files and all directories (starting with the current directory)

One further difference from MS-DOS comes when you try to execute a command of the kind mv *.x (for example, to rename *.x files to *.y). Under Linux, this is not possible with one command. The reason for this restriction is the same as above: the shell substitutes with the list of all files that correspond to the pattern. For *.y, there are no valid file names. The mv command is therefore passed a list of several files *.peter.x *.y and quite understandably, mv can do little with this.

A concrete example: assume that the current directory only contains the files mark.x, peter.x and sandra.x. When you execute mv *.x *.y, the shell substitutes pattern *.x with the three files. The shell does not find any matching files for *.y and passes the pattern as is. Only now is the mv command started. It is passed the following parameters:

```
mv mark.x peter.x sandra.x *.y
```

Even if we passed mark.x peter.x sandra.x peter.y the result would not be the desired one. mv is simply unable to rename several files at a time. Either several files are moved into another directory, or one file is renamed, mv may have some resemblance to the DOS command RENAME, but nothing more.

# Wildcards for advanced users

Unix experts have obviously found a solution to this problem as well: they use the sed stream editor. Because of the rather complicated handling of examples, such as the following should actually be used for shell programming. Here is a brief description of how this works: ls provides the list of files that to be renamed and passes it to sed. sed converts this into a list of cp commands, using the s command (regular find and replace) and passes this list to a new shell, sh, which finally carries out the commands. The line below copies all *.xxx files into *.yy files.