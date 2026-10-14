We can use these commands to see how the if statement works. What the if statement really does is evaluate the success or failure of commands.

```
[me@linuxbox ~]$ if true; then echo "It's true."; fi
It's true.
[me@linuxbox ~]$ if false; then echo "It's true."; fi
[me@linuxbox ~]$
```

The command echo "It's true." is executed when the command following if executes successfully and is not executed when the command following if does not execute successfully. If a list of commands follows if, the last command in the list is evaluated.

```
[me@linuxbox ~]$ if false; true; then echo "It's true."; fi
It's true.
[me@linuxbox ~]$ if true; false; then echo "It's true."; fi
[me@linuxbox ~]$
```

# Using test

By far, the command used most frequently with if is test. The test command performs a variety of checks and comparisons. It has two equivalent forms. The first, shown here:

```
test expression
```

And the second, more popular form, here:

```
[ expression ]
```

where expression is an expression that is evaluated as either true or false. The test command returns an exit status of 0 when the expression is true and a status of 1 when the expression is false.

It is interesting to note that both test and [ are actually commands. In bash they are builtins, but they also exist as programs in /usr/bin for use with other shells. The expression is actually just its arguments with