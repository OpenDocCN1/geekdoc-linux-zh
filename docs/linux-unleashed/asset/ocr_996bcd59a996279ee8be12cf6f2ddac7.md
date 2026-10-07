# # Shell Prompts

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

The first example causes your prompt to be equal to your UNIX username. The second example causes your prompt to be the current working directory. The single quotes are needed here so that the value of the `PWD` variable does not get assigned to the variable only the first time it is executed. If you use double quotes, the `PWD` variable is evaluated only when the command is first entered. (The prompt will always be the directory name

![](bbox=[0.84, 0.295, 0.95, 0.33])

![](bbox=[0.85, 0.34, 0.93, 0.45])