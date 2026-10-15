# 11.11 Command Substitution

Command substitution is used when assigning the output of a command to a variable, or when substituting the output of a command into a string. The Bourne and C shells use backquotes to perform command substitution. The Korn shell does allow the backquote format (calling it "obsolescent"), but placing the command in parentheses is the preferred method because it has simpler quoting rules and makes nesting commands easier.

```
```
Unix/Linux command # Old method with backquotes
$(Unix/Linux command) # New method
```
```

```
```
(Old Way)
1 $ print "The hour is `date +%H`"
The hour is 09
2 $ name=nawk -F: '{print $1}' database
$ print $name
Ebener Scrooge
3 $ ls -l /etc
shutdown
4 $ set `date`
$ set $
5 $ print $*
Sat Oct 13 09:35:21 PDT 2004
6 $ print $2 $6
Oct 2004
```
```

+   1. The output of the date command is substituted into the string.
+   2. The output of the nawk command is assigned to the variable name, and displayed.
+   3. The output of the ls command, enclosed in backquotes, is a list of files from the /etc directory. The filenames will be arguments to the first $ in command. All files with the same name in /etc as are in the current directory are listed.
+   4. The set command assigns the output of the date command to positional parameters. Whitespace separates the list of words into its respective parameters.
+   5. The $ * variable holds all of the parameters. The output of the date command was stored in the $ * variable. Each parameter is separated by whitespace.
+   6. The second and sixth parameters are printed.

> Using backquotes for command substitution is an old form still used in the Bourne and C shells. Although still legal syntax, the Korn shell introduces a new method shown in this section.