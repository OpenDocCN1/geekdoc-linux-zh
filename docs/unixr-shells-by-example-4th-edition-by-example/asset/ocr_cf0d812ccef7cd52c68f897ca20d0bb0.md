# 13.12 Command Substitution

Command substitution is used when assigning the output of a command to a variable or when substituting the output of a command within a string. All shells use backquotes to perform command substitution.¹² Bash allows two forms: the older form, where the command(s) is placed within backquotes, and the new Korn-style form, where the command(s) is placed within a set of parentheses preceded by a dollar sign.

Bash performs the expansion by executing the command and returning the standard output of the command, with any trailing newlines deleted. When the old-style backquote form of substitution is used, the backslash retains its literal meaning except when followed by $, `, or \. When using the $(command) form, all characters between the parentheses make up the command; none are treated specially.

Command substitutions may be nested. To nest when using the old form, the inner backquotes must be escaped with backslashes.

# FORMAT

```
`UNIX command`  # Old method with backquotes
```

```
$(UNIX command)  # New method
```

# EXAMPLE 13.73

(The Old Way)

+   1. $ echo "The hour is `date +%H`"
+      The hour is 09

+   2. $ name=`awk -F: '{print $1}' database`
+      $ echo $name
+      Ebenezer Scrooge

+   3. $ ls `ls /etc`
+      shutdown

+   4. $ set `date`
+      $ echo $*
+      Wed Jul 14 09:35:21 PDT 2004

+   5. $ echo $2 $6
+      Jul 2004

+   6. $ echo `basename \`pwd\``
+      ellie

# EXPLANATION

+   1. The output of the date command is substituted into the string.

+   2. The output of the awk command is assigned to the variable name and displayed.