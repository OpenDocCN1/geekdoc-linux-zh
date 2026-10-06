82 Chapter 3 Tools of the Trade

tells grep to ignore the difference between upper and lowercase when matching the pattern against the lines in intro. Therefore, lines containing the or Or will be printed, as will lines containing THE, THE, tHE, and so on.

Table 3.5 shows other types of regular expressions that you can specify to grep and the types of patterns they'll match.

# Table 3.5 Some grep Examples

| Command | Prints |
| --- | --- |
| grep '[A-Z]' list | Lines from list containing a capital letter |
| grep '[0-9]' data | Lines from data containing a digit |
| grep '[A-Z],...[0-9]' list | Lines from lines containing five-character patterns that start with a capital letter and end with a digit |
| grep '\.pic$' filelist | Lines from fileelist that end with .pic |

# The -v Option

Sometimes you're interested in finding the lines that contain a specified pattern, but those don't. That's what the -v option does for grep: reverse the logic of the matching task. In the example, grep is used to find all the lines in intro that don't contain the pattern UNIX.

```
$ grep -v 'UNIX' intro
Print all lines that do not contain UNIX
Thompson and Dennis Ritchie at Bell Laboratories
in the late 1960s. One of the primary goals in
environment that promoted efficient program
development.
$
```

# The -1 Option

At times, you may not want to see the actual lines that match a pattern but just seek the names of the files that contain the pattern. For example, you have a set of C programs in your current directory (by convention, filenames end with the suffix .c), and you want to know which variable a called Move_history. Here is one way of finding the answer:

```
$ grep 'Move_history' *c
Find Move_history in C source files
exec.c:MOVE cpmove(&Move_history[200] = {0});nexec.c:cpmove(&Move_history[Number_half_moves -1],
exec.c:undo_move(&Move_history[Number_half_moves-1],);
exec.c:cpymove(&last_move, &Move_history[Number_half_moves]);
exec.c:convert_move(&Move_history[Number_half_moves-1]),
exec.c:convert_move(&Move_history[i-1]),
```