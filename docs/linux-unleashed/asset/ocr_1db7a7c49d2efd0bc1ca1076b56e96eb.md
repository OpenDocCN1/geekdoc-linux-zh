# Prompts

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