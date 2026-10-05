# The Command Line 239

```
$ls
hold mark names oldstuff temp zach
house max office personal test
$ls -r
zach temp oldstuff names mark hold
test personal office max house
$ls -x
hold house mark max names office
oldstuff personal temp test zach
$ls -rx
zach test temp personal oldstuff office
names max mark house hold
```

7-1 Using options

present for the command to work. When you do not supply the right number or kind of arguments, cp displays a usage message. Trying cp and then return.

# Options

An option is an argument that modifies the effects of a command. You can frequently specify more than one option, modifying the command in several different ways. Options are specific to and interpreted by the program that the command line calls, not by the shell.

By convention options are separate arguments that follow the name of the command and usually precede other arguments, as filenames. Most utilities require you to prefix options with a single hyphen. However, this requirement is specific to the utility and not the shell. GNU program options are frequently preceded by two hyphens in a row. For example, --help generates a (sometimes extensive) usage message.

7-1 first shows the output of an ls command without any options. ls lists the contents of the working directory in alphabetical order, vertically sorted in columns. When the -r (reverse order) causes the ls utility to display the list of files in reverse alphabetical, sorted in columns. The -x option allows ls to display the list of files in horizontally sorted rows.

When you need to use several options, you can generally group multiple single-letter options into one argument that starts with a single hyphen; do not put spaces between them. You cannot combine options that are preceded by two hyphens in this way. Rules for combining options depend on the program you are running. 7-1 shows both the -r and -x options with the ls. Together these options generate a list of files in horizontally sorted columns, in reverse alphabetical. Most utilities allow you to list options in any order; ls -xr produces the same results as ls -rx. The command ls -x -r also generates the same list.

Some utilities have options that require arguments. For example, the gcc utility has a -o option that must be followed by the name you want to give the executable file gcc generates. Typically an argument to an option is separated from its option letter by a SPACE:

```
$ gcc -o prog.c
```