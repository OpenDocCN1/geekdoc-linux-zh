
## Prompts

bash has two levels of user prompts. The first level is what you see when bash is waiting for a command to be typed. (This is what you normally see when you are working with bash.)

The default first-level prompt is the % character. If you do not like the % character as the prompt or prefer to customize your prompt, you can do so by setting the value of the PS1 bash variable. For example:

```
PS1="Please enter a command"
```

sets the bash shell prompt to the specified string.

The second level of prompt is displayed when bash is expecting more input from you in order to complete a command. The default for the second-level prompt is >. If you want to change the second-level prompt, you can set the value of the PS2 variable, as in:

```
PS2="I need more information"
```

In addition to displaying static character strings in the command prompts (as in the two preceding examples), you can also use some predefined special characters. These special characters place things such as the current time into the prompt. Table 11.1 lists the most commonly used special character codes.

TABLE 11.1. PROMPT SPECIAL CHARACTER CODES.

| Character | Meaning |
| :--- | :--- |
| \! | Displays the history number of this command. |
| \# | Displays the command number of the current command. |
| \$ | Displays a $ in the prompt unless the user is root. When the user is root, it displays a #. |
| \\ | Displays a backslash. |
| \d | Displays the current date. |
| \h | Displays the host name of the computer on which the shell is running. |
| \n | Prints a newline character. This causes the prompt to span more than one line. |
| \nnn | Displays the character that corresponds to the octal value of the number nnn. |
| \s | The name of the shell that is running. |
| \t | Displays the current time. |
| \u | Displays the username of the current user. |
| \w | Displays the base name of the current working directory. |
| \W | Displays the current working directory. |

These special characters can be combined into several useful prompts to provide you with information about where you are. (They can be combined in very grotesque ways, too!) Several examples of setting the PS1 prompt follow here:

```
PS1="\t"
```

This causes the prompt to have the following appearance (there is no space after the prompt):

```
02:16:15
```

The prompt string

```
PS1=\t
```

causes the prompt to have the following appearance:

```
t
```

This shows the importance of including the character sequence in quotation marks. The prompt string

```
PS1="\t\  "
```

causes the prompt to look like this:

```
02:16:30\
```

In this case, there is a space following the prompt because there was a space within the quotation marks.

## Job Control

*Job control* refers to the ability to control the execution behavior of a currently running process. Specifically, you can suspend a running process and cause it to resume running later. bash keeps track of all processes that it starts (as a result of user input) and lets you suspend a running process or restart a suspended one at any time during the life of that process. (For more information on processes, see Chapter 34, “Processes.”)

Pressing Ctrl+Z suspends a running process. The bg command restarts a suspended process in the background, whereas the fg command restarts a process in the foreground.

These commands are most often used when a user wants to run a command in the background but accidentally starts it in the foreground. When a command is started in the foreground, it locks the shell from any further user interaction until the command completes execution. This is usually not a problem because most commands take only a few seconds to execute. If the command you are running takes a long time, though, start the command in the background so that you can continue to use bash to enter other commands in the foreground.

For example, if you start the command find / -name "test" > find.out (which scans the entire file system for files named test and stores the results in a file called find.out) in the foreground, your shell may be tied up for many seconds or even minutes, depending on the size of the file system and the number of users on the system. If you issue this command and want to continue executing in the background so you can use the system again, enter the following:

```
control-z
bg
```

This first suspends the find command, then restarts it in the background. The find command continues to execute, and you have bash back again.

## Customizing bash

Many ways of customizing bash have already been described in this chapter. Until now, the changes that you made affected only the current bash session. As soon as you quit, all of the customizations will be lost. You can, however, make the customizations more permanent by storing them in a bash initialization file.

You can put any commands that you want to be executed each time bash is started into this initialization file. Commands that are typically found in this file are alias commands and variable initializations.

The bash initialization file is named either .profile or .bash_profile, depending on the version of Linux you are using. For simplicity's sake, we'll assume .profile is used, although you should substitute the name your Linux system uses. Each user who uses bash has a .profile file in his home directory. This file is read by bash each time it starts, and all of the commands contained within it are executed.

Many Linux systems use a default profile file (note the lack of a period before the file-name). This file is located in the /etc directory and is read when you start bash. If you want to add your own customizations to bash, you must copy this file into your home directory (if it is not already there) and call it .profile.

**NOTE**

Some setup programs automatically make a copy of the .profile file in your home directory for you when they create your login. However, not all routines do this, so you should check your home directory first. Remember that all files starting with a period are hidden and can only be displayed with the ls -A or ls -a command.

![](img/e8e6b47ac20475e23d48b4c476f5d891_258_0.png)

## bash Command Summary

Some of the most useful commands built into the bash shell are summarized in Table 11.2.

**TABLE 11.2. THE BASH COMMANDS WE'VE USED IN THIS CHAPTER.**

| bash command | What it's used for |
|---|---|
| alias | Used to set bash aliases (command nicknames that can be defined by the user). |
| bg | Background command. Forces a suspended process to continue to execute in the background. |
| cd | Change working directory. This command changes the current working directory to the directory specified as an argument. |
| exit | Terminates the shell. |
| export | Causes the value of a variable to be made visible to all subprocesses that belong to the current shell. |
| fc | Fix command. Used to edit the commands in the current history list. |
| fg | Foreground command. Forces a suspended process to continue to execute in the foreground. |
| help | Displays help information for bash built-in commands. |
| history | Brings up a list of the last n commands that were entered at the command prompt, where n is a configurable variable specifying the number of commands to remember. |
| kill | Used to terminate another process. |
| pwd | Print working directory. Prints the directory in which the user is currently working. |
| unalias | Used to remove aliases that have been defined using the alias command. |

bash has many more commands than are listed here, but these are the most frequently used ones. To see the other commands bash offers and for more details of the commands listed, refer to the bash man page (type `man bash`).

## bash Variables

There are a lot of variables used by bash. Some of the most useful of these variables, including the variable name and a brief description, are shown in Table 11.3.

**TABLE 11.3. THE MOST COMMONLY USED BASH VARIABLES.**

| Variable name | What it's used for |
| :--- | :--- |
| `EDITOR`, `FCEDIT` | The default editor for the `fc`/`bash` command. |
| `HISTFILE` | The file used to store the command history. |
| `HISTSIZE` | The size of the history list. |
| `HOME` | The `HOME` directory of the current user. |
| `OLDPWD` | The previous working directory (the one that was current before the current directory was entered). |
| `PATH` | The search path that bash uses when looking for executable files. |
| `PS1` | The first-level prompt that is displayed on the command line. |
| `PS2` | The second-level prompt that is displayed when a command is expecting more input. |
| `PWD` | The current working directory. |
| `SECONDS` | The number of seconds that have elapsed since the current bash session was started. |

bash has many more variables than are listed here, but the most commonly used ones are shown. To find out the other variables bash offers, call up the man page with the command `man bash`.

## Summary

In this chapter you looked at some of the useful features of the Bourne Again Shell, bash. You have seen how command completion, aliasing, and job control can all combine to make you more productive and efficient when working with bash.
