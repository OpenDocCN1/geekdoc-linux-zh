
## Chapter 12

## Automating System Tasks

### In This Chapter

- Understanding shell scripts
- System initialization
- System start-up and shutdown
- Scheduling system tasks

You’d never get any work done if you had to type every command that needs to be run on your Red Hat Linux system when it starts up. Likewise, you could work more efficiently if you grouped together sets of commands that you run all the time. Shell scripts can handle these tasks.

A shell script is a group of commands, functions, variables, or just about anything else you can use from a shell. These items are typed into a plain-text file. Then that file can be run as a command. Red Hat Linux uses system initialization shell scripts during system start-up to run commands needed to get things going. You can create your own shell scripts to automate the tasks you need to do regularly.

This chapter provides a rudimentary overview of the inner workings of shell scripts and how they can be used. You learn how shell scripts are responsible for the messages that scroll by on the system console during booting and how simple scripts can be harnessed to a scheduling facility (such as cron or at) to simplify administrative tasks.

You also learn to fine-tune your machine to start at the most appropriate run level and to only run the daemons that you need. With that understanding, you’ll be able to personalize your environment and cut down on the amount of time you spend repetitively typing the same commands.

## Understanding Shell Scripts

A shell script is a plain-text file containing a sequence of commands. It can be a simple one-line command that you’d prefer not to type repetitively; a complex program containing several loops, conditional statements, mathematical operations, and control structures; or anything in between.

Shell scripts are equivalent to batch files in DOS/Windows but offer greater flexibility and control through advanced looping constructs, logical operators, functions, and a larger base of commands to use. Shell scripts have much the same syntax as programming languages and are capable of handling many of the same tasks.

Nearly a dozen different shells are available in Red Hat Linux, some of which function virtually identically in an interactive environment. From a programming standpoint, there are basically two varieties, those based on the Bourne shell (sh), and those derived from the C shell (csh). All code and examples in this chapter are based on the bash (Bourne-again shell) environment, which implements a superset of the original Bourne shell. In fact, /bin/sh is a symbolic link to /bin/bash.

The syntax (that is, the way commands and options are constructed) of the C shell is similar to that of the C programming language. It has interactive capabilities that are not included in most Bourne shells. Each shell also uses different configuration files and different methods of setting shell environment variables.

### Executing shell scripts

Shell scripts are files of text commands, functions, environment variables, and/or comments that you can run as commands. In theory, a shell script is a way of grouping a sequence of commands instead of typing them at a shell prompt. In reality, shell scripts can be as complex as any executable program.

An advantage of shell scripts is that they can be opened in any text editor to see what it does. A disadvantage is that shell scripts often execute more slowly than compiled programs. There are two ways to execute a shell script:

- The filename is used as an argument to the shell (e.g., `bash script_file`). In this method, the file does not need to be executable; it just contains a list of shell commands. The shell specified on the command line is used to interpret the commands in the script file. This is most common for quick, simple tasks.
- The shell script is executed by specifying the name of the file on the command line. This requires that the first line of the shell script contain the name of the shell interpreter that is to be used (e.g., `#!/bin/bash` as the first line of the file) and that the execute bit is set. This method is most common for complex scripts that may be used frequently. The first line of a shell script is the only line where the pound sign (#) isn’t interpreted as a comment.

> **CROSS-REFERENCE:** See Chapter 3 for information on `chmod` and `read`/`write`/`execute` file permissions.

The examples in this chapter are of the second variety. When scripts are executed in either manner, options to the program may be specified on the command line. Anything following the name of the script is referred to as a *command-line argument*. These are referenced within the script as the variables $1, $2, $3, … $n. The name of the script itself is held within the variable $0. Note that these are positional parameters, meaning that they refer to a position of information on the command line.

While it is recommended that you choose meaningful variable names, there’s still no substitute for active commenting throughout the design of the shell script. The pound sign (#) prefaces comments and can take up an entire line or exist on the same line as script code.

When you are writing more complex shell scripts, it is best to implement them in stages, making sure the logic is sound at each step before continuing. One way to make sure things are working as expected during testing is to place an echo statement at the beginning of lines within the body of a loop. That way, rather than executing the code, you can see what will be executed without making any permanent changes. Another way to accomplish the same goal is to place dummy echo statements at various places throughout the code. If these lines get printed, you know the correct logic branch is being taken. With the bash shell, you could also use `set -x` near the beginning of the script to display each command that is executed.

Besides commands, shell scripts can contain such components as user-defined variables, program constructs (such as loops and conditionals), and arithmetic instructions. These topics are described in the following sections.

### Creating user-defined variables in shell scripts

Often within a shell script, you want to reuse certain items of information. During the course of processing the shell script, the name or number representing this information may change. To store information used by a shell script in a way that it can be easily reused, you can set variables. Variable names within shell scripts are case-sensitive and can be defined in the following manner:

```bash
NAME=value
```

The first part of a variable is the variable name, and the second part is the value set for that name. For example, you can define a variable containing the city in which you live as follows:

```bash
City="Springfield"
```

Technically, quoting is only necessary to preserve spacing within values, but it may aid in readability. Double quotes (") are considered weak quotes, while single quotes (‘) are considered strong quotes. Any special characters contained in a string surrounded by single quotes (for example, ‘string’) are disabled. With double quotes, however, all special characters are disabled except dollar sign ($), single quote (’), and backslash (\).

Variables can contain the output of a command. The advantage of having a variable set to the output of a command is that you can take advantage of information that changes in certain conditions. In the following example, the MACHINE variable is set to the output of the `uname -n` command. This always sets MACHINE to the name of your current computer, as follows:

```bash
MACHINE=`uname -n`
```

The command contained within the back quotes is executed in a subshell, and the output is stored in the variable name. In this case, the `uname -n` command outputs the computer's host name (such as `baskets.handonghistory.com`) and assigns that value to the MACHINE variable.

> **NOTE:** A subshell provides a way to execute a command, or series of commands, outside of the current shell. The subshell is similar to the current shell in that it remembers locations of commands and values of environment variables from the parent shell. However, changes to the subshell's environment are not automatically passed back to the parent shell.

Variables can also take on the values of other variables. This is a way of taking advantage of changing information as the shell script runs. For example, a shell script could determine an account balance ($CurrentBalance) and then store that value in the BALANCE variable, enabling the value to be saved as follows:

```bash
BALANCE=$CurrentBalance
```

> **NOTE:** When being assigned, only the variable name is necessary. When being referenced, the variable name must be prefaced by a dollar sign ($).

### Performing arithmetic evaluation in shell scripts

While variables in shell scripts can contain numbers, all values are treated as alphanumeric strings unless otherwise instructed by the built-in *type set* command. Integer arithmetic can be performed using the built-in `let` command or through the external `expr` command. For example, given that the variable BIGNUM contains the value 1024, the following two commands would both store the value 64 in the RESULT variable:

```bash
let Result=$BIGNUM/16
Result=`expr $BIGNUM / 16`
```

> **NOTE:** While most elements of shell scripts are relatively free form (where white space, such as spaces or tabs, is insignificant), both of the previous commands are particular about spacing. The `let` command insists on no spaces between each operand and the mathematical operator, whereas the syntax of the `expr` command requires white space between each operand and its operator.

Valid mathematical operations available in bash's built-in `let` command are listed in Table 12-1 in order of decreasing precedence. Multiple operators in the same row indicate equal precedence. Table 12-2 similarly lists the valid mathematical operators for the `expr` command.
