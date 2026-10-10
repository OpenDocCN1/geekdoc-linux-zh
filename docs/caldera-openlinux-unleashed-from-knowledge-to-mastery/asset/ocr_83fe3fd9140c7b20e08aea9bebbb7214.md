The first form uses double-quotes. Double-quotes disable word separators. The following is a rewritten form of the backslash substitution example:

```
`set price "Price:\n\$4.45 a box."`
```

Note that it is no longer necessary to put backslashes before the spaces, but it is still necessary to escape the dollar sign. Inside double-quotes, variable, command, and backslash substitution still occurs.

The second form of quoting is **brace quoting**. Placing text between braces turns off practically all substitution. For example,

```
```
set price {Price}
$4.45 a box.
```

```

In this example, we do not need to backslash-escape anything. Furthermore, to insert a newline, we need a literal newline in the script. The sequence `\n` inside braces would yield the two characters `\n` unchanged.

Note that braces nest and that backslash-escaped braces do not count for brace matching. Nevertheless, the backslash will not be removed.

# ## Comments

If the first non-blank character of a line is `#`, it and all characters following it up to a newline are treated as a comment and discarded. If the `#` character appears anywhere else in a command (other than the first non-blank character), it is not treated as a comment.

# ## Variables

Variables in Tcl are created automatically when they are assigned. They do not have types; everything in Tcl is treated as a string. You can think of variables as named storage bins that can store a value.

# **Note**

Actually, the latest version of Tcl does not treat everything as a string internally. But, from the point of view of the Tcl programmer, it is convenient to think of everything as being stored as a string.

You can name a variable anything, but it is common to name variables as sequences of letters and digits, starting with a letter.

The `set` command creates variables. The first form takes two arguments (a variable name and a value) and sets the variable to the specified value. The return value of the