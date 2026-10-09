
## Arguments

On the command line each sequence of nonblank characters is called a *token* or *word*. An *argument* is a token that a command acts on (e.g., a filename, a string of characters, a number). For example, the argument to a *vim* or *emacs* command is the name of the file you want to edit.

The following command line uses *cp* to copy the file named *temp* to *tempcopy*:

```
$ cp temp tempcopy
```

Arguments are numbered starting with the command itself, which is argument zero. In this example, *cp* is argument zero, *temp* is argument one, and *tempcopy* is argument two. The *cp* utility requires at least two arguments on the command line. Argument one is the name of an existing file. In this case, argument two is the name of the file that *cp* is creating or overwriting. Here the arguments are not optional; both arguments must be present for the command to work. When you do not supply the right number or kind of arguments, *cp* displays a usage message. Try typing *cp* and then pressing **RETURN**.

## Options

An *option* is an argument that modifies the effects of a command. These arguments are called options because they are usually optional. You can frequently specify more than one option, modifying the command in several ways. Options are specific to and interpreted by the program that the command line calls, not the shell.

By convention, options are separate arguments that follow the name of the command and usually precede other arguments, such as filenames. Many utilities require options to be prefixed with a single hyphen. However, this requirement is specific to the utility and not the shell. GNU long (multicharacter) program options are frequently prefixed with two hyphens. For example, *--help* generates a (sometimes extensive) usage message.

The first of the following commands shows the output of an *ls* command without any options. By default, *ls* lists the contents of the working directory in alphabetical order, vertically sorted in columns. Next the *ls -r* (reverse order; because this is a GNU utility, you can also specify *-reverse*) option causes the *ls* utility to display the list of files in reverse alphabetical order, still sorted in columns. The *ls -x* option causes *ls* to display the list of files in horizontally sorted rows.

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

**Combining options** When you need to use several options, you can usually group multiple single-letter options into one argument that starts with a single hyphen; do not put SPACES between the options. You cannot combine options that are preceded by two hyphens in this way. Specific rules for combining options depend on the program you are running. The next example shows both the -t and -x options with the ls utility. Together these options generate a list of filenames in horizontally sorted rows in reverse alphabetical order.

```
$ ls -rx
zach    test    temp    personal    oldstuff    office
names   max     mark    house       hold
```

Most utilities allow you to list options in any order; thus ls -xr produces the same results as ls -rx. The command ls -x -r also generates the same list.

### The --help option

**tip** Many utilities display a (sometimes extensive) help message when you call them with an argument of --help. All utilities developed by the GNU Project (page 3) accept this option. Following is the help message displayed by the bzip2 compression utility (page 245).

```
$ bzip2 --help
bzip2, a block-sorting file compressor.  Version 1.0.6, 6-Sep-2010.

usage: bunzip2 [flags and input files in any order]

-h  --help      print this message
-Z  --decompression      force decompression
-z  --compress  force compression
-k  --keep    keep (don't delete) input files
-f  --force   overwrite existing output files
...
If invoked as 'bzip2', default action is to compress.
as 'bunzip2', default action is to decompress.
as 'bzcat', default action is to decompress to stdout.
...
```

**Option arguments** Some utilities have options that require arguments. These arguments are not optional. For example, the gcc utility (C compiler) has a -o (output) option that must be followed by the name you want to give the executable file that gcc generates. Typically an argument to an option is separated from its option letter by a SPACE:

```
$ gcc -o prog prog.c
```

Some utilities sometimes require an equal sign between an option and its argument. For example, you can specify the width of output from diff in two ways:

```
$ diff -W 60 filea fileb
*or*
$ diff -W width=60 filea fileb
```

**Arguments that start with a hyphen** Another convention allows utilities to work with arguments, such as filenames, that start with a hyphen. If a file named -ls is in the working directory, the following command is ambiguous:

```
$ ls -1
```

This command could be a request to display a long listing of all files in the working directory (-l option) or a request for a listing of the file named -l. The ls utility interprets it as the former. Avoid creating a file whose name begins with a hyphen. If you do create such a file, many utilities follow the convention that a -- argument (two consecutive hyphens) indicates the end of the options (and the beginning of the arguments). To disambiguate the preceding command, you can type

```
$ ls -- -1
```

Using two consecutive hyphens to indicate the end of the options is a convention, not a hard-and-fast rule, and a number of utilities do not follow it (e.g., find). Following this convention makes it easier for users to work with a program you write.

### Displaying readable file sizes: the -h option

> Most utilities that report on file sizes specify the size of a file in bytes. Bytes work well when you are dealing with smaller files, but the numbers can be difficult to read when you are working with file sizes that are measured in gigabytes or terabytes. Use the -h (or --human-readable) option to display file sizes in kilobytes, megabytes, gigabytes, and terabytes. Experiment with the df -h (disk free) and ls -lh commands.

For utilities that do not follow this convention, there are other ways to specify a filename that begins with a hyphen. You can use a period to refer to the working directory and a slash to indicate the following filename refers to a file in the working directory:

```
$ ls ./-1
```

You can also specify the absolute pathname of the file:

```
$ ls /home/max/-1
```

## SIMPLE COMMANDS

This section expands on the discussion of command-line syntax that starts on page 144.

A simple command comprises zero or more variable assignments followed by a command line. It is terminated by a control operator (e.g., &, ;, ||, NEWLINE; page 341). A simple command has the following syntax:

```
[name=value ...] command-line
```

The shell assigns a value to each name and places it in the environment (page 1032) of the program that command-line calls so it is available to the called program and its children as a variable. The shell evaluates the name=value pairs from left to right, so if name appears more than once in this list, the rightmost value takes precedence.

The **command-line** might include redirection operators such as > and < (page 153). The exit status (page 1029) of a simple command is its return value.

The following commands demonstrate how you can assign a value to a name (variable) and place that name in the environment of a child program; the variable is not available to the interactive shell you are running (the parent program). The script named `echo_ee` displays the value of the variable named ee. The first call to `echo_ee` shows ee is not set in the child shell running the script. When the call to `echo_ee` is preceded by assigning a value to ee, the script displays the value of ee in the child shell. The final command shows ee has not been set in the interactive shell.

```
$ cat echo_ee
echo 'The value of the ee variable is: $ee'
$ ./echo_ee
The value of the ee variable is: 
$ ee=88 ./echo_ee
The value of the ee variable is: 88
$ echo $ee
$
```

## PROCESSING THE COMMAND LINE

As you enter a command line, the tty device driver (part of the Linux kernel) examines each character to see whether it must take immediate action. When you press **CONTROL-H** (to erase a character) or **CONTROL-U** (to kill a line), the device driver immediately adjusts the command line as required; the shell never sees the character(s) you erased or the line you killed. Often a similar adjustment occurs when you press **CONTROL-W** (to erase a word). When the character you entered does not require immediate action, the device driver stores the character in a buffer and waits for additional characters. When you press **RETURN**, the device driver passes the command line to the shell for processing.

When the shell processes a command line, it looks at the line as a whole and *parses* (breaks) it into its component parts (Figure 5-1). Next the shell looks for the name of the command. Usually the name of the command is the first item on the command line after the prompt (argument zero). The shell takes the first characters on the command line up to the first blank ( **TAB** or **SPACE**) and then looks for a command with that name. The command name (the first token) can be specified on the command line either as a simple filename or as a pathname. For example, you can call the `ls` command in either of the following ways:

```
$ ls
or
$ /bin/ls
```
