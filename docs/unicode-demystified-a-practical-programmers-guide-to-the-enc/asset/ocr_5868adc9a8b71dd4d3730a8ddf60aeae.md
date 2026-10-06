# Command Line Expansion

$ prefix=Alex
$ echo prefix is short for ${prefix}ander.
Alex is short for Alexander.

Without braces prefix would have to be separated from ander with a SPACE so that the shell would recognize prefix as a variable. This change would cause Alexander to become Alex ander.

# Tilde Expansion

Chapter 4 shows a shorthand notation to specify your home directory or the home directory of another user (page 116). This section provides a more detailed explanation of tilde expansion

The tilde ( is a special character when it appears at the start of a token on a command line. When it sees this type of tilde, the shell looks for the string of characters—up to the first slash (/) or to the end of the word if there is no slash—as a possible login name. If this possible login name is null (that is, if the tilde appeared as a word itself or if it was immediately followed by a slash), the shell substitutes the value of the HOME variable for the tilde. In other words the shell expands the tilde into the value of HOME. The following example demonstrates this substitution or expansion, with the last command copying the file named letter from Alex's home directory to the working directory.

```
$ echo $HOME
/home/alex
$ echo -
/home/alex
$ echo -letter
/home/alex/letter
$ cp ~/letter .
```

If a string of characters forms a valid login name, the shell substitutes the path of the home directory associated with that login name for the tilde and the name. If it is not null and not a valid login name, the shell does not make any substitution:

```
$ echo ~jenny
/home/jenny
$ echo ~root
/root
$ echo ~xx
~xx
```

# Parameter Expansion

Parameter expansion occurs when the shell replaces a dollar sign followed by one or more digits with the value of the positional parameter corresponding to the