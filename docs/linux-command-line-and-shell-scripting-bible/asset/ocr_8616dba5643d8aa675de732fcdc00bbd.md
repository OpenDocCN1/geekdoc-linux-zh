```
$ printf "%%A, %%B, %%d, %%Y)T\n" $value
Thursday, January 31, 2008
$ printf "%%F\n" $value
Thu Jan 31 12:42:11 EST 2008
$
```

It's pretty amazing what you can do with the %T format control code!

# # Scripting in the ksh93 Shell

For the most part, scripting in the ksh93 shell isn't much different than the bash shell. Most of your bash shell should work just fine in a ksh93 shell environment, and the ones that don't just need a little modification.

If you're writing scripts for the ksh93 shell, there are a few additional things that you can use to make life a little easier for you. This section describes the major differences you'll find between the ksh93 shell and the bash shell.

# # Mathematical operations

A great feature of the ksh93 shell is the ease with which you can use mathematical operations. This section describes the features available in the ksh93 shell for manipulating numbers and performing mathematical operations.

# # Performing calculations

Mathematical calculations are performed using one of two methods:

+   - The let command
- Double parentheses

The let command allows you to assign the result of a mathematical operation directly to a variable:

```
$ let value=4*5
$ echo $value
20
$
```

Using this format, you can't have any spaces between the equal sign and the equation elements. Alternatively, you can enclose the equation in double quotation marks and use as many spaces as you want:

```
$ let value="4 * 3"
$ echo $value
12
$
```