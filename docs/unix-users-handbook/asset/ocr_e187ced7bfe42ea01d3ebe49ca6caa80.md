![](bbox=[0.03, 0.205, 0.12, 0.298])

Every time you type **h**, the history command is executed.

The following example creates an alias of a command that con- tains spaces, so the command is surrounded by single quotes:

```
```
alias ls='ls -al'
alias
ls
```
```

The first command creates an alias for "ls" that executes the **ls -al** command. We then issued the **alias** command to see whether indeed the new alias appears in the list of aliases. Then we run **ls** to see whether **ls -al** is run.

You don’t have to keep an alias for the duration of your session after having set it. If you don’t like an alias you can use the **unalias** command to remove an alias.

To see **unalias** work let’s again produce a list of aliases, use **unalias** to unset the **h** alias, and run the **h** command to see if indeed it has been removed.

```
```
unalias h
h
```
```

When we issued **unalias** to remove the **h** alias and then try to run *h*, we were told that *h* is not found.

![](bbox=[0.03, 0.644, 0.12, 0.746])

```
```
sys1 3:alias proc 'echo "Number of processes are: \c";
ps -ef | wc -l'
			# single quote on outside
			# double quote on inside
```
```

When you run **proc**, you see the following:

```
```
sys1 4: proc
Number of processes are: 44
```
```

A lot of quoting takes place in this command line. To understand what is taking place on this line turn to Table 7-3 for help.