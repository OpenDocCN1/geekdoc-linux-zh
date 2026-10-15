# Table 15.2 Proper Double Quoting Examples

| C Shell | Bourne Shell | Korn Shell |
|---|---|---|
| echo "Hello $LOGNAME!" | echo "Hello $LOGNAME!" | print "Hello $LOGNAME!" |
| echo "I don't care" | echo "I don't care" | print "I don't care" |
| echo "The date is `date`" | echo "The date is `date`" | print "The date is $(date)" |
| echo "\\" | echo "\\" | print "\\" |
| \\\\ | \ | \ |

# Backquotes

Backquotes are used in shell programs for command substitution. They are unrelated to single and double quotes, but often the source of problems. For example, when copying a shell script, if the backquotes are replaced with single quotes (merely by misreading the code), the program will no longer work.

# EXAMPLE 15.10

```
#!/bin/sh
1 now=`date`
2 echo Today is $now
3 echo "You have `ls|wc -l` files in this directory"
4 echo 'You have `ls|wc -l` files in this directory'

(Output)
2 Today is Mon Jul 5 10:24:06 PST 2004
3 You have 33 files in this directory
4 You have `ls|wc -l` files in this directory
```

# EXPLANATION

+   1 The variable now is assigned to the output of the UNIX/Linux date command. (For the T/C shell: set now = `date`.) The backquotes cause command substitution. The backquote is normally found under the tilde (~) on your keyboard.
+   2 The value of variable now is displayed with the current date.
+   3 The backquotes surround a UNIX/Linux pipe. The output of ls is piped to wc -l. The result is to count the number of files listed in this directory. Double quotes around the string will not interfere with command substitution. The output is embedded in the string and printed.
+   4 By enclosing the string in single quotes, the backquotes are not interpreted, but treated as literal characters.