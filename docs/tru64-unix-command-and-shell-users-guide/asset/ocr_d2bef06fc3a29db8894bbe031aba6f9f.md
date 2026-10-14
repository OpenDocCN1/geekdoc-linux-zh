```
/random/
?
-
```

Once you have searched for a string, you can search for the same string again by entering // . The following example shows one search for the string only, and then a second search for the same string:

```
/only/
The only way to stop
//
line that contains only
-
```

# B.5.2 Searching Backward Through the Buffer

Searching backward through the buffer is much like searching forward, except that you enclose the string in question marks (?):

```
?appending?
appending is to enter a
-
```

The context search begins on the first line before the current line, and locates the first line that contains the string appending. That line becomes the current line. If ed searches the entire buffer without finding the string, it stops the search at the current line and displays the message ?.

Once you have searched backward for a string, you can search backward for the same string again by entering ??. This is because ed remembers search strings.

# B.5.3 Changing the Direction of a Search

You can change the direction of a search for a particular string by using the slash (/) and question mark (?) search characters alternately:

```
/only/
line that contains only
??
The only way to stop
-
```

If you go too far while searching for a character string, it is convenient to be able to change the direction of your search.

# B.6 Making Substitutions – The s (substitute) Subcommand

Use the s (substitute) subcommand to replace a character string (a group of one or more characters) with another. The s subcommand works with