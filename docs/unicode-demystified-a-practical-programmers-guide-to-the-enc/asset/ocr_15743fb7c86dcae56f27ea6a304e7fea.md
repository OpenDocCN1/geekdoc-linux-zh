# Syntax

Command line syntax dictates the ordering and separation of the elements on a command line. When you press the RETURN key after entering a command, the shell scans the command line for proper syntax. The syntax for a basic command line is

```
command [arg1] [arg2] ... [argn] RETURN
```

One or more SPACES must appear between elements on the command line. The command- is the command name, arg1 through argn are arguments, and RETURN is the keystroke that terminates all command lines. The command line syntax is enclosed in brackets to show that they are optional. Not all commands require arguments: Some commands do not allow arguments; other commands allow a variable number of arguments; and others require a specific number of arguments. Options, a special kind of argument, are usually preceded by a hyphen (also called a dash or minus sign: -). (No smiley [page 1492] intended).

# Command Name

Some useful GNU/Linux command lines consist of only the name of the command without any arguments. For example, is by itself lists the contents of the working directory. Most commands accept one or more arguments. Commands that require arguments typically give a short error message, called a usage message, when you use them without arguments, with incorrect arguments, or with the wrong number of arguments.

# Arguments

On the command line each sequence of nonblank characters is called a token, or word. An argument is a token, such as a filename, string of text, number, or other object that a command acts on. For example, the argument to a vi or emacs-command is the name of the file you want to edit.

The following command line shows cp copying the file name to tempcopy:

```
$ cp temp tempcopy
```

Arguments are numbered starting with the command itself as argument zero. In this example cp is argument zero, temp is argument one, and tempcopy is argument two. The cp utility requires two arguments on the command line. (The utility can take more not fewer: see Part III.) Argument one is the name of an existing file, and argument two is the name of the file that cp is creating or overwriting. Here the arguments are not optional; both arguments must be present for the command to