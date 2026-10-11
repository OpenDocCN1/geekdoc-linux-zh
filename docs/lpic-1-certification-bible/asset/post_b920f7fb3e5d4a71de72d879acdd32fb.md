
alias ls='ls --color=auto'
#alias ll='ls -l'
#alias la='ls -A'
#alias l='ls -CF'
#alias dir='ls --color=auto --format=vertical'
#alias vdir='ls --color=auto --format=long'
# set a fancy prompt
PS1='\u@\h:\w\$ '
fi

As you can see in the previous example of .bash_profile, it is common to source the .bashrc file so that it is read at login, too. Normally the .bashrc holds user-defined aliases and functions.

> In the Real World
> Many Linux distributions have the .bash_profile file source the .bashrc file. Aliases are normally stored in .bashrc.

### The .bash_logout file

The .bash_logout file is executed when the user logs out. The following is an example:

# -/ .bash_logout: executed by bash(1) when login shell exits.
# When leaving the console clear the screen to increase privacy
case " $tty " in
/dev/tty[0-9]) clear
esac

By default this file usually clears the screen so the next user does not see what the previous user did. Put any cleanup tasks that you want done at logout in this file.

### The .inputrc file

The ~ / .inputrc file is used to customize the readline. If it is not found, the /etc/inputrc file is used. Below is an example of the /etc/inputrc file.

# do not bell on tab-completion
#set bell-style none
set meta-flag on
set input-meta on
set convert-meta off
set output-meta on
"\e0d": backward-word
"\e0c": forward-word
# for linux console
"\e[1~": beginning-of-line
"\e[4~": end-of-line
"\e[5~": beginning-of-history
"\e[6~": end-of-history
" \e[3-": delete-char
" \e[2-": quoted-insert
# for xterm
" \eOH": beginning-of-line
" \eOF": end-of-line
#for freebsd console
" \e[H": beginning-of-line
" \e[F": end-of-line

Chapter 2 covers the readline library in detail.

### Options

Shell options control many different parameters that define how the shell operates. Some examples of these settings are the style of text editing, file overwrite protection, and variable handling. To enable an option, use the following:

set -o optionname

To disable an option, use the following:

set +o optionname

No, that is not a typo. The dash enables an option, and the plus disables an option. Most options are disabled by default. Table 14-12 lists some of the most common options.

> **Exam Tip** The -o parameter is used to enable an option, while +o is used to disable an option.

**Table 14-12 set Options**

| Option | Function |
| :--- | :--- |
| alllexport | Automatically exports all variables created. |
| braceexpand | The shell does brace expansion. This is on by default. |
| emacs | Uses the emacs-style mode for command-line editing. This is on by default. |
| errexit | Exits immediately if a simple command exits with a nonzero status. |
| hashall | Remembers the location of commands when they are executed to speed future searches. This is on by default. |
| histexpand | Enables ! style history substitution. This is on by default. |

**Table 14-12 (continued)**

| Option | Function |
| :--- | :--- |
| history | Enables command history. |
| ignoreeof | Ignores the Ctrl-D command, which normally exits the shell. |
| noclobber | Does not allow file redirection such as > to overwrite an existing file. |
| noexec | Reads commands but does not execute them. |
| noglob | Does not expand wildcards like * and ?. |
| nounset | Reports an error when an unnamed variable is used. Normally an unnamed variable is reported as having a value of "". |
| vi | Uses the vi-style command-line editing mode. |

Another way to set shell options is with the shopt command, which was introduced with bash version 2. Table 14-13 lists the command-line options for shopt. Using the -o option you can use shopt to set those options previously set with the set command.

**Table 14-13 shopt Command-Line Options**

| Option | Function |
| :--- | :--- |
| -s | Sets each option. |
| -u | Unsets each option. |
| -q | Suppresses normal output. Enables quiet mode. |
| -o | Allows the values of the option names to be those used by the set command. Used for backward compatibility. |
| -p | Displays a list of the settable options and their current values. |

A list of the most common options is shown in Table 14-14. Most options are disabled by default.

**Table 14-14 shopt Options**

| Option | Function |
| :--- | :--- |
| cdable_vars | If set, an argument to the cd command that is not a valid directory is assumed to be a variable with a value of the directory you want to change to. |
| cdspell | If set, minor spelling errors when using cd in directory names will be corrected. |
| checkhash | If set, bash first checks to see if an executable listed in the hash table exists before executing. If it no longer exists, a standard path search is done. |
| cmdhist | If set, bash attempts to save all lines of a multiple-line command in the same history entry. |
| dotglob | If set, bash includes filenames beginning with a . in the results of path name expansion. |
| histappend | If set, the history list is appended to the history file at exit, instead of overwriting it. |
| mailwarn | If set, if bash does a mail check and notices that the mail file has been accessed since the last check, a warning is issued. |

## Writing Simple Scripts

### 1.9 Shells, Scripting, Programming, Compiling

- **Customize or write simple scripts.** Customize existing scripts (like paths in scripts of any language), or write simple new (*bash*) scripts. Besides use of standard *sh* syntax (loops, tests), be able to do things like: command substitution and testing of command return values, test of file status, and conditional mailing to the superuser. Make sure the correct interpreter is called on the first (*#!*) line, and consider location, ownership, and execution- and suid-rights of the script.

Shell scripts are used to execute several commands in a sequence. They are similar to batch files in the Microsoft world, but provide much more power and control. They are stored as text files and can be as simple as a list of commands to execute or can utilize much more complex functions and structures.

## Starting a shell script

Shell scripts are written differently for different shells. This is important to remember if you use the more complex functions of scripting. The scripts in this section are geared toward bash, since it is the default shell for Linux and is the most used.

The first line of a shell script tells the system which interpreter to use. It begins with `#!`, which denotes the interpreter. An example is the following:

#!/bin/bash

There is no space anywhere in the line. This line should be found only once in any script. It tells the system that the /bin/bash interpreter should be used when executing. If a script is written for another interpreter such as the ksh shell, or perl, this line will be different. If you are unsure which language a script is written in, it is often useful to just check the first line.

> The first line of a shell script tells the system which interpreter to use when the script is run.

## Writing a basic script

You can start with a basic script, as shown in the following example. For this example, pretend that you do not know about aliases.

#!/bin/bash
# This is a simple script that can be used to display
# my documents in a folder, while pausing the output.
ls -al *.doc | more

As you can see, this is a simple script that runs `ls` with basic parameters. To make this script executable, you need to do the following:

chmod u+x script_name

`chmod` is covered in Chapter 6.

The script can also be run manually without making it executable. For example:

bash script_name

The `#` signs at the beginning of lines denote comments, except for the first line, which tells the system which interpreter to use. Be sure to use comments often in scripts so that later when editing them again, you can remember what you were doing.
