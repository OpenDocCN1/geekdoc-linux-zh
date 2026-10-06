The subscript is a text value, similar to the key in the associative array. The values can be any text or numerical values:

```
$ test3=( fruit=banana vegetable=carrot age=18)
$
```

Once you assign the subscripts and values, you can reference an individual subscript value with the format:

```
variable.subscript
```

Here's how this looks:

```
$ echo $(test3.fruit)
banana
$ echo $(test3.age)
18
$
```

Each individual subscript value can be extracted by referencing the subscript name with the variable.

# Special variable subscripts

There are several special subscripts that are available in the ksh93 shell. These subscripts define current information about the shell, as well as current information about the currently running process in the shell. Table 22-4 lists the special ksh93 shell variables.

Since the subscript variables use periods in their names, you must use braces around them when referencing them:

```
$ echo ${.sh.version}
Version M 1993-12-28 r-
$
```

The subscript variables used in discipline functions are discussed later in the "Discipline functions" section.

# Built-in commands

The ksh93 built-in commands should look a lot like the bash commands, since they're based on the Bourne shell. Table 22-5 shows the ksh93 built-in commands.

As you will, the ksh93 contains a fair amount of built-in commands, making it a robust shell to use for scripting. You should recognize most of these commands from the bash shell.

The ksh93 uses the echo, print and printf commands for displaying data and text. The differences among these three commands can get confusing at times.

The echo command in ksh93 is somewhat unreliable. For the most part, it behaves similarly to the bash, but it's not guaranteed. Only the most basic use of the echo command is