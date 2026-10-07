
# Lab 1.2: Setting Up Your Interactive Environment

c) What (if anything) printed?

Answer: If FPATH is set up correctly, you will see a colon-separated list of directories, including at least your ~/fun directory.

If the correct information was not displayed, using the same logic as in the discussion about PATH, you need to add a command such as the following to your ~/.profile:

```
export FPATH=$FPATH:~/fun
```

![](img/694fa9f0320e707804a4c650b96a09b4_41_0.png)

If /etc/profile does not have a command to assign a value to FPATH (on some systems it does, and on some systems it doesn't), you will end up with a colon (:) at the beginning of your FPATH value, which the shell will interpret as “the current directory followed by the remaining directories in the value string. “That, it’s the same as having dot (.) at the beginning of your FPATH. The same thing holds for PATH. If you don't want this behavior, you will need to use one of the parameter expansions covered in Chapter 10, “Patterns, Expansions, and Substitutions,” to deal with the problem.

Run the following command to check whether you have an environment file:

```
print "My environment file is $ENV"
```

d) What printed?

Answer: If the variable ENV is set, you should see the name of your environment file. If not, you will see only the first part of the message. Your interaction might look something like the following:

```
$ print "My environment file is: $ENV"
```

```
My environment file is: /home/vickery/.kshrc
```

```
$
```

If nothing prints after the colon (:) in the message, it means there is no ENV= in your ~/.profile, so add the following command to that file (or one similar to it if you prefer to use a different file name):

```
export ENV=~/.kshrc
```

Normally, there is no need to export ENV, but it doesn’t do any harm, and there are some situations where it actually is needed to get your interactive shell to process the commands in your environment file.

# Chapter 1: SETTING UP 23

At this point, you don't know about functions, aliases, or the set command, which are the commands you would normally put in an environment file, so to get you started, we'll just show you an example without explaining the contents. As you learn more features of the shell, you can develop your own version of this file. Note that the following file contains sample personal preferences that you should modify to match your way of working.

print This is .kshrc

```
# Set up to use arrow keys for command line editing
EDITOR=vim # Editor to invoke from inside more
VISUAL=emacs # Command line editing style
emacs_keybind # Make arrow keys work
```

# Set up to use less instead of more

```
PAGER=less
export LS='-Eapn?f&?f .?m(File %i of %m) \
..?lt1lb/b%L:?pt&b\:?bt&B/%B:-..?e(end)?xNext:\n%x..
```

# Redefine the ls and rm commands for interactive use.

```
LSFLAGS=-F # Put slashes after directory names, etc.
RMFLAGS=-i # Always ask before deleting files
```

```
alias ls="command ls $LSFLAGS"
alias rm="command rm $RMFLAGS"
```

# Set some shell options

```
set -nolog # Keep function defs out of history file
set -o noclobber # Don't overwrite existing files
```

# Add some command names -- aliases

```
alias="cd .." # Go up one directory
alias m=$PAGER # more (or less)
alias md=mkdir # Like DOS
alias rd=rmdir # Like DOS
alias q=exit # 
```

# Add some new command names -- functions

# Lab 1.2: Setting Up Your Interactive Environment

```
function l1 {
  ls -l "$@" | $PAGER
}
function la {
  ls -la "$@" | $PAGER
}
```

It's common practice in UNIX systems for programs to read commands from a file when they start up to set up user's preferences for the program. Such files typically have names that begin with ~. (to make them hidden files in the user's home directory), followed by the name of the program (ksh, in this case), followed by rc (short for “read commands”). Knowing this can remove some of the mystery from looking at a list of the hidden files in your home directory.

# LAB 1.2 SELF-REVIEW QUESTIONS

To test your progress, you should be able to answer the following questions:

- 1) What is the environment of a process?
  a) The computer that executes it.
  b) The user who runs it.
  c) The other programs in memory at the same time.
  d) A list of variables with associated values.
  e) Its network neighborhood.

- 2) What is an environment variable?
  a) A name and its associated value that is part of a process's environment.
  b) A peripheral device that works in different ways at different times.
  c) A peripheral device that always works the same way.
  d) A symbol that is exported to a process.
  e) None of the above. 

- 3) What does it mean to export?
  a) To send a variable to another.

b) To send a copy to another.
  c) To make its name available to children.
  d) To make its name available to parents.
  e) None of the above.

- 4) The Shell always reads .kshrc if it exists.
  a) True
  b) False, because it never reads that file.
  c) False, because it reads that only if its name is.
  d) False, because it reads that only if it exists.
  e) None of the above.

- 5) Use the numbers 1-6 to indicate the sequence in which events occur:
  a) The shell executes the environment.
  b) Login reads the password.
  c) The shell executes ~/.profile.
  d) The shell executes /etc/profile.
  e) The shell executes the name.
  f) The shell prints a prompt and waits for the user to type.

# LAB 1.3 

# EDITING AND RUNNING SCRIPTS AND FUNCTIONS

# LAB OBJECTIVES

After this lab, you will be able to:

- Define and Run a Script
- "Dot" a Script
- Define and Run a Function

There are two kinds of shell programs, scripts and functions. A script is a list of commands that you put into a file that the shell processes by reading the file. The /etc/profile and ~/.profile are examples of scripts, albeit special ones, because the shell executes them. The scripts we will be concerned with here are the ones you write to create new commands. If you put a set of commands in a file and have everything set up properly, you can use the name of the script as a new command. Just type its name, and the shell will execute the commands inside it.

There are two ways to run a script. You can run it as a command that has its own, private environment, or you can run it so that it shares the environment of your interactive shell's process. You will learn about setting up and running scripts both ways in this lab.

Functions are normally smaller pieces of code that also provide new commands you can use. The key difference between a script and a function is that once the shell reads the definition of a function, it keeps a copy of it in its own address space (memory), so that running the script takes less time. Scripts, on the other hand, are read from their disk files every time they are run.

This lab will make sure you are set up to run scripts and functions properly.

# LAB 1.3 EXERCISES

# I.3.1 DEFINE AND RUN A SCRIPT

For a script file to work as a command, the file containing the script must be in one of the directories listed in your PATH (or you must type the complete pathname of the script file), and the file must be executable. At this point, ~/bin is a directory that is listed in your PATH, so all you need to do to define and run a script is to create an executable file in that directory.

Run the following sequence of commands. (Expect to see two error messages).

Be sure you don't already have a file named s131 in your bin directory.

```
s131
> bin/s131
s131
chmod +x bin/s131
s131
```
