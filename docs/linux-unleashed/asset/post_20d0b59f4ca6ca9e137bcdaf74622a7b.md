
## Output Redirection

Output redirection is more commonly used than input redirection. Output redirection enables you to redirect the output from a command into a file, as opposed to having the output displayed on the screen.

There are many situations in which this capability can be very useful. For example, if the output of a command is quite large and does not fit on the screen, you may want to redirect it to a file so you can view it later using a text editor. Output redirection is done in much the same way as input redirection. Instead of using the `<` symbol, the `>` symbol is used.

To redirect the output of an `ls` command into a file named `directory.out`, the following command is used:

```
ls > directory.out
```

## Pipelines

Pipelines are a way to string together a series of commands. This means that the output from the first command in the pipeline is used as the input to the second command. You can tell `pdksh` to create a pipeline by typing two or more commands separated by the `|` character. The following is an example of using a `pdksh` pipeline:

```
cat test.file | sort | uniq
```

This is a fairly common pipeline. Here, the contents of `test.file` (the output from the `cat` command) are fed into the input of the `sort` command. The `sort` command, without any options, sorts its input alphabetically by the first field in the input. The sorted file is then piped into the `uniq` command. The `uniq` command removes any duplicate lines from the input. If `test.file` contains the lines

```
Sample dialog
Hello there
How are you today
Hello there
I am fine
```

the output from the pipeline is the following:

```
Hello there
How are you today
I am fine
Sample dialog
```

All of the lines in the file have been sorted by the first word in the line, and one of the `Hello` there lines has been removed because of the `uniq` command.

## Shell Prompts

pdksh has three levels of user prompts. The first level is what the user sees when the shell is waiting for a command to be typed. (This is what you normally see when you are working with the shell.) The default prompt is the $ character. If you do not like the dollar sign as the prompt or prefer to customize the prompt, you can do so by setting the value of the `PS1` pdksh variable.

To set a variable, give the name and equal sign, and the string you want to set it to. Make sure you do not place any spaces on either side of the equal sign or the shell will not interpret your command properly. For example, the line

```
PS1="! Tell me what to do"
```

sets the shell prompt to the string `! Tell me what to do`. The pdksh shell keeps track of how many commands have been entered since it was started. This number is stored into the shell variable called `!`. When you include the `!` in the prompt, it displays the current command number in the prompt. The previous prompt command causes the command number followed by the string `Tell me what to do` to be displayed on the command line each time pdksh is expecting you to enter a command.

The second level prompt is displayed when pdksh is expecting more input from you in order to complete a command. The default for the second level prompt is `>`. If you want to change the second level prompt, you can do so by setting the value of the `PS2` pdksh variable, as in the following example:

```
PS2=" I need more information"
```

This causes the string `I need more information` to be displayed on the command line whenever pdksh needs something from you to complete a command.

pdksh does not support the advanced prompt options that bash supports. There is no pre-defined set of escape codes that you can put in a pdksh prompt variable to display such items as the time or current working directory. You can, however, put other pdksh variables into a prompt variable. For example, the following two prompts are valid:

```
PS1=" (LOGNAME) "
PS1=' ($PWD )'
```

The first example causes your prompt to be equal to your UNIX username. The second example causes your prompt to be the current working directory. The single quotes are needed here so that the value of the `PWD` variable does not get assigned to the variable only the first time it is executed. If you use double quotes, the `PWD` variable is evaluated only when the command is first entered. (The prompt will always be the directory name of the directory that you are in when you enter the command.) The single quotes cause the value of the `PS1` variable to be equal to the current value of the `PWD` variable. For more information on using these quotes, see Chapter 14, “Shell Programming.”

## Job Control

Job control is the capability to control the execution behavior of a currently running process. Specifically, you can suspend a running process and cause it to resume running at a later time. The `pksh` shell keeps track of all of the processes that it starts, and you can suspend a running process or restart a suspended one at any time during the life of that process.

Pressing the `Ctrl+Z` key sequence suspends a running process. The `bg` command restarts a suspended process in the background and the `fg` command restarts a process in the foreground.

These commands are most often used when a user wants to run a command in the background but accidentally starts it in the foreground. When a command is started in the foreground, it locks the shell from any further user interaction until the command completes execution. This is usually not a problem because most commands take only a few seconds to execute. If the command you are running is going to take a long time, you typically start the command in the background so that you can continue to use `pksh` to enter other commands while it completes running.

If you start a command in the foreground that is going to take a long time, your shell may be tied up for several minutes. If you have done this and want to continue executing the command in the background, enter the following:

```
control-z
bg
```

This suspends the command and restarts it in the background. The command continues to execute and you have control of `pksh`.

## Key Bindings

One useful feature that `pksh` supports, which is lacking in the Bourne Again Shell, is *key bindings*. This feature enables you to change the behavior of key combinations for the purpose of command-line editing.

If, for example, you do not like the fact that you have to use the *emacs* key sequence Ctrl+P to move up in the history buffer, you can change the key sequence for that command to something else. The syntax for doing the key binding is the following:

```
bind <key sequence> <command>
```

This feature effectively enables you to customize *pdksh* to have the exact feel that you want. One of the most commonly used key bindings is to bind the *up*, *down*, *left*, and *right arrows* to be used as they are in *bash* (for scrolling up and down the history list, and for moving left and right along the command line). This binding is typically found in your .kshrc file, which is the startup file for the shell (it is read whenever the shell starts).

The *bind* commands that are needed to create these bindings are as follows:

```
bind '^[''=prefix-2
bind '^XA'=up-history
bind '^XB'=down-history
bind '^XC'=forward-char
bind '^XD'=backward-char
```

Table 12.1 gives some of the most useful editing commands that you can use for binding keys, along with the default binding and a description of each. You can get a listing of all of the editing commands that *pdksh* supports by typing the *bind* command without any arguments.

### TABLE 12.1. USEFUL KEY BINDINGS FOR PDKSH.

| Keystroke | Meaning |
| :--- | :--- |
| abort (^G) | Used to abort another editing command. It is most commonly used to stop a history list search. |
| backward-char (^B) | Moves the cursor backward one character. This command is often bound to the left arrow key. |
| backward-word (^[b) | Moves the cursor backward to the beginning of a word. |
| beginning-of-line (^A) | Moves the cursor to the beginning of the command line. |
| complete (^[\^) | Tells pdksh to try to complete the current command. |
| copy-last-arg (^[_) | Causes the last word of the previous command to be inserted at the cursor position. |

*continues*
