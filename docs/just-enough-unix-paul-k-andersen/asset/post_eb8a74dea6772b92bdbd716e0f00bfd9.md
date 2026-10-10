
## 22.11 Review (Continued)

12. `vi .login`
13. `source .login`
14. `vi .login`
15. `source .login`
16. `vi calendar`
17. `source .login`
18. `vi .cshrc`
19. `. .cshrc`
20. `h`

2. **Repeat the most recent command on the list.** This is done by typing two exclamation marks at the prompt. Try it:

   `/home/you > !!` `Return`

   You should see another listing of commands, as before.

3. **Repeat a command by number.** Thus, to repeat the seventh command on the list, type

   `/home/you > !7` `Return`

   The command line will appear on the screen, and the command will be run.

   `echo "Your wish is my command, Oh Great One."`
   `Your wish is my command, Oh Great One.`

4. **Repeat a command by entering the first letter(s) of the command line.** Thus, to repeat a command line that starts with the letter $s$, type

   `/home/you > !s` `Return`

   The most recent command beginning with $s$ is the *source* command:

   `source .login`

### 22.12 Command Summary

**Checking the Values of Variables**

| Command | Description |
| :--- | :--- |
| `setenv` | list the values of environment variables |
| `set` | list the values of special `csh` variables |
| `echo $var` | print value of variable `var` |

**Setting Values of Variables**

| Command | Description |
| :--- | :--- |
| `set var = value` | set variable `var` to `value` |
| `set var = "A word"` | store string `A word` in variable `var` |
| `setenv VAR value` | set environment variable `VAR` to `value` |

**Executing a Startup File**

| Command | Description |
| :--- | :--- |
| `source .login` | execute `.login` |

**Changing Prompts**

| Command | Description |
| :--- | :--- |
| `set prompt = "Prompt string"` | set prompt to `Prompt string` |

**Creating Command Aliases (csh)**

| Command | Description |
| :--- | :--- |
| `alias c command` | make `c` an alias for `command` |
| `unalias c` | remove `c` as an alias for `command` |

**Using the history Mechanism (csh)**

| Command | Description |
| :--- | :--- |
| `history` | print `history` list |
| `!!` | repeat most recent event on `history` list |
| `!n` | repeat the `n`th event on `history` list |
| `!abc` | repeat the most recent event starting with letters `abc` |

### 22.13 Exercises

1. The `date` command prints the date and current time. Add the following line to your `.login`, making sure to use backquotes around `date`:

   ```
   `echo "The date and time are `date`."`
   ```

   Exit the editor and run the `.login` using the `source` command. What happens?

2. The backquotes were needed in the previous exercise to tell the shell that date was to be interpreted as a command, not as a word. What happens if the back-quotes are omitted? Try it. Open up your `.login` and remove the backquotes from `date`:

   ```
   echo "The date and time are date"
   ```

   Exit the editor and run the `.login` using the `source` command. What happens? (Now open up the file and replace the backquotes.)

3. What is your search path?

4. What is the complete pathname for your shell?

5. Change your prompt so that it always displays the current working directory.

6. The `rm`, `cp`, and `mv` commands are dangerous because they can overwrite or remove existing files. The `-i` ("interactive") option will ask you to confirm that this is what you want. If the `-i` option is available to you, put the following lines in your `.cshrc` file:

   ```
   alias rm "rm -i"
   alias cp "cp -i"
   alias mv "mv -i"
   ```

7. Explain what the following lines would do if they were placed in your `.cshrc` file:

   ```
   alias m more
   alias f finger
   alias ls 'ls -R'
   ```

8. To prevent files from being overwritten by the redirection operation, place the following line in your `.cshrc`:

   ```
   set noclobber
   ```

   Does this work as expected?

# PART VII: SHELL SCRIPTS

## 23 SHELL SCRIPTS

Until now, you have been giving commands to the UNIX shell by typing them on the keyboard. When used this way, the shell is said to be a command interpreter. The shell can also be used as a high-level programming language. Instead of entering commands one at a time in response to the shell prompt, you can put a number of commands in a file, to be executed all at once by the shell. A program consisting of shell commands is called a *shell script*. This chapter will introduce you to shell scripts for the Bourne Shell.

### 23.1 Simple Shell Script

Suppose you were to make up a file named `commands` containing the following lines:

```shell
# A simple shell script
cal
date
who
```

The first line in this file begins with a `#` symbol, which indicates a *comment line*. Anything following the `#` is ignored by the shell. The remaining three lines are shell commands: the first produces a calendar for the current month, the second gives the current date and time, and the third lists the users currently logged onto your system.

One way to get the Bourne Shell (`sh`) to run these commands is to type:

```
$ sh < commands
```

The redirection operator `<` tells the shell to read from the file `commands` instead of from the standard input. It turns out, however, that the redirection symbol is not really needed in this case. Thus, you can also run the commands file by typing:

```
$ sh commands
```

### 23.2 Subshells

Is there any way to set up `commands` so that you can run it without explicitly invoking the shell? In other words, can you run `commands` without first typing `sh`, `csh`, or `ksh`? The answer is yes, but you first have to make the file *executable*. The `chmod` utility does this:

```
$ chmod u+x commands
```

The argument `u+x` tells `chmod` that you want to add (+) permission for the user (u) to execute (x) the shell script in the file. Now all you need do is type the file name:

```
$ commands
```

and the shell will run the commands in the file.

When you tell the shell to run a script such as the `commands` file, your login shell actually calls up another shell process to run the script. (**Remember,** the shell is just another program, and UNIX can run more than one program at a time.) The parent shell waits for its child to finish, then takes over and gives you a prompt:

```
$
```

Incidentally, a subshell can be different from its parent shell. For example, you can have `csh` or `ksh` as your login shell, but use `sh` to run your shell scripts. Many users in fact do this. When it comes time to run a script, the `csh` or `ksh` simply calls up `sh` as a subshell to do the job.

We will always use `sh` for running shell scripts. To make sure that `sh` is used, we will include the following line at the top of each shell script file:

```
#!/bin/sh
```

Thus, our `commands` file would look something like this:

```shell
#!/bin/sh
# A simple shell script
cal
date
who
```

### 23.3 The Shell as a Programming Language

The sample script `commands` is almost trivial---it does nothing more than execute three simple commands that you could just as easily type into the standard input. The shell can actually do much more. It is, in fact, a sophisticated programming language, with many of the same features found in other programming languages, including

- Variables
- Input/output functions
- Arithmetic operations
- Conditional expressions
- Selection structures
- Repetition structures

We will discuss each of these in order.

### 23.4 Variables

There are three types of variables commonly used in Bourne Shell scripts:

- *Environment Variables*. Sometimes called special shell variables, keyword variables, predefined shell variables, or standard shell variables, they are used to tailor the operating environment to suit your needs. Examples include `TERM`, `HOME`, and `MAIL`.
- *User-created Variables*. These are variables that you create yourself.
- *Positional Parameters*. These are used by the shell to store the values of command-line arguments.

Of these, the environment variables and user-created variables have been introduced already. The positional parameters, however, are new, and since they are very useful in shell programming, we will examine them in some detail now.

The positional parameters are also called *read-only variables*, or *automatic variables*, because the shell sets them for you automatically. They “capture” the values of the command-line arguments that are to be used by a shell script. The positional parameters are numbered 0, 1, 2, 3,... , 9. To illustrate our use, consider the following shell script, and assume that it is contained in an executable file named `echo_args`:

```shell
#!/bin/sh
# Illustrate the use of positional parameters
echo $0 $1 $2 $3 $4 $5 $6 $7 $8 $9
```
