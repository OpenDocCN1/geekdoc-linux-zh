To make a substitution at the beginning of a line, use the s/newstring/ subcommand. In the following example, one s subcommand adds the string "Remember" to the start of line number 1. Another s subcommand adds the string "adding" to the start of line 2:

```
1s/^/Remember,/p
Remember, The only way to quit
2s/^/adding/p
adding text is to enter a
-
```

To make a substitution at the end of a line, use a subcommand of the form s/$/newstring/. In the following example, the s subcommand adds the string "Then press Enter." to the end of line number 4:

```
4s/$/  Then press Enter./p
a dot.  Then press Enter.
-
```

Notice that the substituted string includes two blanks before the word Then to separate the two sentences.

# B.6.7 Using a Context Search

If you do not know the number of the line you want to change, you can locate it with a context search. See Section B.5 for more information on context searches.

For convenience, you can combine a context search and a substitution into a single subcommand in the following format:

```
/string to find/ s/ oldstring / newstring /
```

In the following example, ed locates the line that contains the string ", The" and replaces that string with ", the":

```
/, The/s/, The/, the/p
Remember, the only way to quit
-
```

Also, you can use the search string as the string to be replaced with a subcommand of the form /string to find/ s//newstring/. In the following example, ed locates the line that contains the string "cONtains ONLy", replaces that string with "contains only", and prints the changed line:

```
/cONtains ONLy/s//contains only/p
line that contains only
-
```