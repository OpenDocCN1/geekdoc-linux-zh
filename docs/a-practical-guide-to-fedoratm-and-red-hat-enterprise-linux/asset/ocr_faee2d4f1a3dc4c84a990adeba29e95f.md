# ## Arguments

On the command line each sequence of nonblank characters is called a *token* or *word*. An *argument* is a token that a command acts on (e.g., a filename, a string of characters, a number). For example, the argument to a *vim* or *emacs* command is the name of the file you want to edit.

The following command line uses *cp* to copy the file named *temp* to *tempcopy*:

```
```
$ cp temp tempcopy
```
```

Arguments are numbered starting with the command itself, which is argument zero. In this example, *cp* is argument zero, *temp* is argument one, and *tempcopy* is argument two. The *cp* utility requires at least two arguments on the command line. Argument one is the name of an existing file. In this case, argument two is the name of the file that *cp* is creating or overwriting. Here the arguments are not optional; both arguments must be present for the command to work. When you do not supply the right number or kind of arguments, *cp* displays a usage message. Try typing *cp* and then pressing **RETURN**.

# ## Options

An *option* is an argument that modifies the effects of a command. These arguments are called options because they are usually optional. You can frequently specify more than one option, modifying the command in several ways. Options are specific to and interpreted by the program that the command line calls, not the shell.

By convention, options are separate arguments that follow the name of the command and usually precede other arguments, such as filenames. Many utilities require options to be prefixed with a single hyphen. However, this requirement is specific to the utility and not the shell. GNU long (multicharacter) program options are frequently prefixed with two hyphens. For example, *--help* generates a (sometimes extensive) usage message.

The first of the following commands shows the output of an *ls* command without any options. By default, *ls* lists the contents of the working directory in alphabetical order, vertically sorted in columns. Next the *ls -r* (reverse order; because this is a GNU utility, you can also specify *-reverse*) option causes the *ls* utility to display the list of files in reverse alphabetical order, still sorted in columns. The *ls -x* option causes *ls* to display the list of files in horizontally sorted rows.

```
```
$ ls
hold      mark      names       oldstuff    temp        zach
house     max       office      personal    test
$ ls -r
zach      temp      oldstuff    names       mark        hold
test      personal  office      max         house
$ ls -x
hold      house     mark        max         names       office
oldstuff  personal  temp        test        zach
```
```