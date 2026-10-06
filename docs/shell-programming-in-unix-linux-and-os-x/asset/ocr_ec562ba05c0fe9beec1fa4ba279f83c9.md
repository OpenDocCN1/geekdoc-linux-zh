# Variables 101

both have the same effect of assigning the null value to dataflag and have added the benefit that it looks like it's deliberate, rather than in the first instance where it might be perceived later as a mistake or typo.

Be advised that the assignment

dataflag = "

is not equivalent to the three previous ones because it assigns a single space character to dataflag; that's different from assigning no characters to it.

# Filename Substitution and Variables

Here's a puzzle for you: If you type

x=*

will the shell store the character * into the variable x, or will it store the names of all the files in your current directory into the variable x? Let's try out and see:

```
$ ls
What files do we have?
```

```
addresses
intro
lotspaces
names
nu
numbers
phonebook
stat
$ x=\n$ echo $x
addresses intro lotsaSpaces names nu numbers phonebook stat
$
```

There's a lot to be learned from this simple example. Was the list of files stored into the variable x when

x=*

was executed, or did the shell do the substitution when

```
echo $x
```

was executed?

It turns out the shell does not perform filename substitution when assigning values to variables.

x=*

assigns the single character * to x. This means that given the output shown, the shell must have done the filename substitution when executing the echo command. In fact, the precise sequence of steps that occurred when

```
echo $x
```