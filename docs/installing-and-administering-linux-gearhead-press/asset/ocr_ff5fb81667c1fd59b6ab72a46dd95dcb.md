Now, he sees three of the four possible files listed. Still, he observes, this way is not an efficient method for obtaining a comprehensive listing of hidden .bash files, either.

# The Exclamation Point as a Wildcard

You use the exclamation point (!) within square brackets as a wildcard to exclude possibilities. Again, the position defined by the location of the brackets is expanded by the shell but to only one character, as shown in Example 7.13. Unlike the square list brackets, however, only filenames whose characters in that position are *not* members of the set of characters specified within the brackets are used as input to the command.

It might help to think of ! as meaning *not*.

> **WARNING** Using wildcards with certain commands, especially the rm (remove) command, can be risky. You might get unexpected and unwelcome results. We recommend that you use the interactive form (that is, rm -i) when you want to include wildcards. This recommendation is especially helpful when you want to introduce recursive options (-R) that might alter the contents of directories all the way down the directory tree.

# Example 7.13 The Exclamation Point (!) and Bracket [] Wildcards

Continuing from Example 7.12, Perez makes a copy of his .bash_history file but renames the copy .bash-history (with a hyphen in the middle instead of an underscore). Then, he enters the same command he used in Example 7.12 to find all possible .bash files with either a hyphen or an underscore in the middle:

```
$ cp .bash_history .bash-history<Enter>
$ echo .bash[-_] *<Enter>
.bash_history .bash-history .bash_logout .bash_profile
```

Now, he decides to use the exclamation point wildcard to exclude the new .bash-history file, as such:

```
$ echo .bash[!-_*]<Enter>
.bash_history .bash_logout .bash_profile
```

His exclamation point tells the shell to ignore the .bash files, which have hyphens in the middle. The result: He sees the same three files as he saw in Example 7.12. The shell, predictably, has ignored the .bash-history file.