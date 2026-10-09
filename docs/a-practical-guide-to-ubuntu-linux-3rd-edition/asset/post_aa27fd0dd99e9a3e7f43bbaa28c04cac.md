
Technique 1 requires that the working directory be in the PATH variable. Techniques 1 and 2 require that you have execute and read permission for the file holding the script. Technique 3 requires that you have read permission for the file holding the script.

## Job Control

A job is one or more commands connected by pipes. You can bring a job running in the background into the foreground using the `fg` builtin. You can put a foreground job into the background using the `bg` builtin, provided that you first suspend the job by pressing the suspend key (typically CONTROL-Z). Use the `jobs` builtin to see which jobs are running or suspended.

## Variables

The shell allows you to define variables. You can declare and initialize a variable by assigning a value to it; you can remove a variable declaration using `unset`. Variables are local to a process unless they are exported using the `export` builtin to make them available to child processes. Variables you declare are called user-created variables. The shell defines keyword variables. Within a shell script you can work with the command-line (positional) parameters the script was called with.

## Process

Each process has a unique identification (PID) number and is the execution of a single Linux command. When you give it a command, the shell forks a new (child) process to execute the command, unless the command is built into the shell. While the child process is running, the shell is in a state called sleep. By ending a command line with an ampersand (&), you can run a child process in the background and bypass the sleep state so that the shell prompt returns immediately after you press RETURN. Each command in a shell script forms a separate process, each of which may in turn fork other processes. When a process terminates, it returns its exit status to its parent process. An exit status of zero signifies success; nonzero signifies failure.

## History

The history mechanism, a feature adapted from the C Shell, maintains a list of recently issued command lines, also called events, that provides a way to reexecute previous commands quickly. There are several ways to work with the history list; one of the easiest is to use a command-line editor.

## Command-line Editors

When using an interactive Bourne Again Shell, you can edit a command line and commands from the history file, using either of the Bourne Again Shell's command-line editors (`vim` or `emacs`). When you use the `vim` command-line editor, you start in Insert mode, unlike `vim`. You can switch between Command and Input modes. The `emacs` editor is modelless and distinguishes commands from editor input by recognizing control characters as commands.

## Aliases

An alias is a name that the shell translates into another name or (complex) command. Aliases allow you to define new commands by substituting a string for the first token of a simple command.

## Functions

A shell function is a series of commands that, unlike a shell script, is parsed prior to being stored in memory. As a consequence shell functions run faster than shell scripts. Shell scripts are parsed at runtime and are stored on disk. A function can be defined on the command line or within a shell script. If you want the function definition to remain in effect across login sessions, you can define it in a start-up file. Like functions in many programming languages, a shell function is called by giving its name followed by any arguments.

# EXERCISES

1. Explain the following unexpected result:

```bash
$ whereis date
date: /bin/date ...
$ echo $PATH
./usr/local/bin:/usr/bin:/bin
$ cat > date
echo "This is my own version of date."
$ ./date
Fri May 21 11:45:49 PDT 2010
```

2. What are two ways you can execute a shell script when you do not have execute permission for the file containing the script? Can you execute a shell script if you do not have read permission for the file containing the script?

3. What is the purpose of the PATH variable?

   a. Set the PATH variable so that it causes the shell to search the following directories in order:
   - `/usr/local/bin`
   - `/usr/bin`
   - `/bin`
   - `/usr/kerberos/bin`
   - The `bin` directory in your home directory
   - The working directory

   b. If there is a file named `doit` in `/usr/bin` and another file with the same name in your `~/bin` directory, which one will be executed? (Assume that you have execute permission for both files.)

   c. If your `PATH` variable is not set to search the working directory, how can you execute a program located there?

   d. Which command can you use to add the directory `/usr/games` to the end of the list of directories in `PATH`?

4. Assume you have made the following assignment:

```bash
$ person=zach
```

Give the output of each of the following commands:

   a. `echo $person`
   b. `echo '$person'`
   c. `echo "$person"`

5. The following shell script adds entries to a file named `journal-file` in your home directory. This script helps you keep track of phone conversations and meetings.

```bash
$ cat journal
# journal: add journal entries to the file
# $HOME/journal-file

file=$HOME/journal-file
date >> $file
echo -n "Enter name of person or group: "
read name
echo "$name" >> $file
echo >> $file
cat >> $file
echo "--------------------------------------------" >> $file
echo >> $file
```

   a. What do you have to do to the script to be able to execute it?
   b. Why does the script use the `read` builtin the first time it accepts input from the terminal and the `cat` utility the second time?

6. Assume the `/home/zach/grants/biblios` and `/home/zach/biblios` directories exist. Give Zach's working directory after he executes each sequence of commands given. Explain what happens in each case.

   a.

```bash
$ pwd
/home/zach/grants
$ CDPATH= $(pwd)
$ cd
$ cd biblios
```

   b.

```bash
$ pwd
/home/zach/grants
$ CDPATH=$(pwd)
$ cd $HOME/biblios
```

7. Name two ways you can identify the PID number of the login shell.

8. Give the following command:

```bash
$ sleep 30 | cat /etc/inittab
```

Is there any output from `sleep`? Where does `cat` get its input from? What has to happen before the shell displays another prompt?

# ADVANCED EXERCISES

9. Write a sequence of commands or a script that demonstrates variable expansion occurs before pathname expansion.

10. Write a shell script that outputs the name of the shell executing it.

11. Explain the behavior of the following shell script:

```bash
$ cat quote_demo
twoliner="This is line 1.
This is line 2."
echo "$twoliner"
echo $twoliner
```

   a. How many arguments does each `echo` command see in this script? Explain.

   b. Redefine the IFS shell variable so that the output of the second `echo` is the same as the first.

12. Add the exit status of the previous command to your prompt so that it behaves similarly to the following:

```bash
$ [0] ls xxx
15: xxx: No such file or directory
$ [1]
```

13. The `dirname` utility treats its argument as a pathname and writes to standard output the path prefix—that is, everything up to but not including the last component:

```bash
$ dirname a/b/c/d
a/b/c
```

If you give `dirname` a simple filename (no `/` characters) as an argument, `dirname` writes a `.` to standard output:

```bash
$ dirname simple
.
```

Implement `dirname` as a bash function. Make sure that it behaves sensibly when given such arguments as `/`.

14. Implement the `basename` utility, which writes the last component of its pathname argument to standard output, as a bash function. For example, given the pathname `a/b/c/d`, `basename` writes `d` to standard output:

```bash
$ basename a/b/c/d
d
```

15. The Linux `basename` utility has an optional second argument. If you give the command `basename path suffix`, `basename` removes the suffix and the prefix from `path`:

```bash
$ basename src/shellfiles/prog.bash .bash
prog
$ basename src/shellfiles/prog.bash .c
prog.bash
```

Add this feature to the function you wrote for exercise 14.
