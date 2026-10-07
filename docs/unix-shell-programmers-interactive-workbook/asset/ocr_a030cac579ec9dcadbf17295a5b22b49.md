# Chapter 4: Simple Variables 185

The first command assigns the value Kalamazoo, a string of characters, to the variable named city.

The second command prints a reference to to the variable city, followed by a comma, a space, and the letters MI. The braces aren't really necessary in the second line because the comma unambiguously marks the end of the variable name, but using braces makes seeing the end of the variable name earlier.

Using braces around all variable names is a bother when you are working interactively, but doing so in scripts is a good idea because it makes the code bit easier to read. It's not so much of a bother to type the braces in a script because you type the command once, then run it any number of times.

Assign Syracuse to the variable city and the value NY to the variable state in one command line, then use references to these variables to print Syracuse, NY.

+   c) What command line did you enter?

Answer:You should have used the following two commands:
$ city=Syracuse=NY
$ print $(city), $(state)
Syracuse, NY
$

The first line makes two variable assignments in one command line, but it's not necessary. You could put a semicolon between them, but it's line prints the values of the two variables, along with a comma and a space between them.

Note that the commas in this and the previous item there are just so they will be printed.They aren't part of the variables in any way.

Assign Minot and ND to city and state, then print the new values.

+   d) What single command line would accomplish this?

Answer:There are two ways you could do this, illustrating a subtle point about how the shell processes assignment commands: