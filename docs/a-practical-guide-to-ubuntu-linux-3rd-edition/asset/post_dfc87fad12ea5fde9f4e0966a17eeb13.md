
## 7. The Shell

### In This Chapter
- The Command Line . . . . . . . . . . 238
- Standard Input and Standard Output . . . . . . . . . . 243
- Pipes . . . . . . . . . . . . . . . . . . 251
- Running a Command in the Background . . . . . . . . . . . 254
- kill: Aborting a Background Job . . . 255
- Filename Generation/Pathname Expansion . . . . . . . . . . . 256
- Builtins . . . . . . . . . . . . . . . . . . . . . . . . 261

This chapter takes a close look at the shell and explains how to use some of its features. For example, it discusses command-line syntax. It also describes how the shell processes a command line and initiates execution of a program. In addition the chapter explains how to redirect input to and output from a command, construct pipes and filters on the command line, and run a command in the background. The final section covers filename expansion and explains how you can use this feature in your everyday work.

The exact wording of the shell output differs from shell to shell: What your shell displays may differ slightly from what appears in this book. Refer to Chapter 9 for more information on **bash** and to Chapter 27 for information on writing and executing **bash** shell scripts.

### The Command Line

The shell executes a program when you give it a command in response to its prompt. For example, when you give the ls command, the shell executes the utility program named ls. You can cause the shell to execute other types of programs—such as shell scripts, application programs, and programs you have written—in the same way. The line that contains the command, including any arguments, is called the command line. This book uses the term command to refer to both the characters you type on the command line and the program that action invokes.

### Syntax

Command-line syntax dictates the ordering and separation of the elements on a command line. When you press the RETURN key after entering a command, the shell scans the command line for proper syntax. The syntax for a basic command line is

```
command [arg1] [arg2] ... [argn] RETURN
```

One or more SPACES must separate elements on the command line. The command is the name of the command, arg1 through argn are arguments, and RETURN is the keystroke that terminates all command lines. The brackets in the command-line syntax indicate that the arguments they enclose are optional. Not all commands require arguments: Some commands do not allow arguments; other commands allow a variable number of arguments; and still others require a specific number of arguments. Options, a special kind of argument, are usually preceded by one or two hyphens (also called a dash or minus sign: -).

### Command Name

![](img/2344fc4a798f29dca9e8b5ed7288171a_288_0.png)

Some useful Linux command lines consist of only the name of the command without any arguments. For example, ls by itself lists the contents of the working directory. Commands that require arguments typically give a short error message, called a usage message, when you use them without arguments, with incorrect arguments, or with the wrong number of arguments.

### Arguments

On the command line each sequence of nonblank characters is called a token or word. An argument is a token, such as a filename, string of text, number, or other object that a command acts on. For example, the argument to a vim or emacs command is the name of the file you want to edit.

The following command line shows cp copying the file named temp to tempcopy:

```
$ cp temp tempcopy
```

Arguments are numbered starting with the command itself, which is argument zero. In this example, cp is argument zero, temp is argument one, and tempcopy is argument two. The cp utility requires at least two arguments on the command line. Argument one is the name of an existing file. Argument two is the name of the file that cp is creating or overwriting. Here the arguments are not optional; both arguments must be present for the command to work. When you do not supply the right number or kind of arguments, *cp* displays a usage message. Try typing *cp* and then pressing RETURN.

### Options

An option is an argument that modifies the effects of a command. You can frequently specify more than one option, modifying the command in several different ways. Options are specific to and interpreted by the program that the command line calls, not by the shell.

By convention options are separate arguments that follow the name of the command and usually precede other arguments, such as filenames. Most utilities require you to prefix options with a single hyphen. However, this requirement is specific to the utility and not the shell. GNU program options are frequently preceded by two hyphens in a row. For example, *\-\-help* generates a (sometimes extensive) usage message.

Figure 7-1 first shows the output of an *ls* command without any options. By default *ls* lists the contents of the working directory in alphabetical order, vertically sorted in columns. Next the *-r* (reverse order; because this is a GNU utility, you can also use *--reverse*) option causes the *ls* utility to display the list of files in reverse alphabetical order, still sorted in columns. The *-x* option causes *ls* to display the list of files in horizontally sorted rows.

When you need to use several options, you can usually group multiple single-letter options into one argument that starts with a single hyphen; do not put SPACES between the options. You cannot combine options that are preceded by two hyphens in this way. Specific rules for combining options depend on the program you are running. Figure 7-1 shows both the *-r* and *-x* options with the *ls* utility. Together these options generate a list of filenames in horizontally sorted columns, in reverse alphabetical order. Most utilities allow you to list options in any order; thus *ls -xr* produces the same results as *ls -rx*. The command *ls -x-r* also generates the same list.

Some utilities have options that themselves require arguments. For example, the *gcc* utility has a *-o* option that must be followed by the name you want to give the executable file that *gcc* generates. Typically an argument to an option is separated from its option letter by a SPACE:

```
$ gcc -o prog prog.c
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_288_0.png)

### Displaying readable file sizes: the `-h` option

**tip** Most utilities that report on file sizes specify the size of a file in bytes. Bytes work well when you are dealing with smaller files, but the numbers can be difficult to read when you are working with file sizes that are measured in megabytes or gigabytes. Use the `-h` (or `--human-readable`) option to display file sizes in kilo-, mega-, and gigabytes. Experiment with the `df -h` (disk free) and `ls -lh` commands.

Another convention allows utilities to work with arguments, such as filenames, that start with a hyphen. If a file's name is `-l`, the following command is ambiguous:

```
$ ls -l
```

This command could mean a long listing of all files in the working directory or a listing of the file named `-l`. It is interpreted as the former. Avoid creating files whose names begin with hyphens. If you do create them, many utilities follow the convention that a `--` argument (two consecutive hyphens) indicates the end of the options (and the beginning of the arguments). To disambiguate the command, you can type

```
$ ls -- -l
```

You can use an alternative format in which the period refers to the working directory and the slash indicates that the name refers to a file in the working directory:

```
$ ls ./-l
```

Assuming that you are working in the /home/max directory, the preceding command is functionally equivalent to

```
$ ls /home/max/-l
```

The following command displays a long listing of this file:

```
$ ls -l -- -l
```

These are conventions, not hard-and-fast rules, and a number of utilities do not follow them (e.g., *find*). Following such conventions is a good idea; it becomes much easier for users to work with your program. When you write shell programs that require options, follow the Linux option conventions.

### Processing the Command Line

As you enter a command line, the Linux tty device driver (part of the Linux kernel) examines each character to see whether it must take immediate action. When you press **CONTROL-H** (to erase a character) or **CONTROL-U** (to kill a line), the device driver immediately adjusts the command line as required; the shell never sees the character(s) you erased or the line you killed. Often a similar adjustment occurs when you press **CONTROL-W** (to erase a word). When the character you entered does not require immediate action, the device driver stores the character in a buffer and waits for additional characters. When you press **RETURN**, the device driver passes the command line to the shell for processing.

When the shell processes a command line, it looks at the line as a whole and **parses** (breaks) it into its component parts (Figure 7-2). Next the shell looks for the name of the command. Usually the name of the command is the first item on the command
