If you wanted the previous output to be sunflowers are pretty then you would need to eliminate the space between the value of the variable sn and the word flowers. As you can see in the following example, the obvious solution to this problem doesn't work:

```
$ echo $snflowers are pretty
are pretty
```

Just removing the space on the command line has caused the shell to treat the new word snflowers as a variable name, and one which currently has no value. The standard way round this problem is to enclose the required variable name in a pair of curly braces, thus separating the name from the following word, but without having a space between them:

```
$ echo ${sn}flowers are pretty
sunflowers are pretty
```

In general, it is acceptable to change the value of an existing variable just by re-assigning it a new value:

```
$ sn=`all kinds of `
$ echo ${sn}flowers are pretty
all kinds of flowers are pretty
```

In this example, the quotes around the string being assigned to the variable sn are needed because the string is to contain spaces. Normally, the shell will split a line of input into separate words, using the spaces as the split points. In this example it is required that the string of characters, including its spaces, all be assigned to the shell variable.

Sometimes you will want to declare a variable, set it to a particular value and then want to prevent that value from being changed. This can be done by setting the variable up as readonly, once its initial value has been assigned:

```
$ readonly sn
$ sn=sun
bash: sn: read-only variable
$ echo ${sn}flowers are pretty
all kinds of flowers are pretty
```

As another example, there is also a standard shell variable, which you have already seen, that is set up as readonly – the UID variable. This obviously needs to be readonly as its value is set when the user logs in, from the user's UID in the password file, and is not a value which can just be changed at will.

Whenever you create a variable it is just local to the current shell. This means that the values of your local shell variables cannot be seen by other commands or scripts run from your shell. Quite often, it would be useful for these values to be made available to the commands that the shell executes. This can be done with the command export. In the previous example, the variable sn is a local variable, which can be made available to subsequent commands as follows: