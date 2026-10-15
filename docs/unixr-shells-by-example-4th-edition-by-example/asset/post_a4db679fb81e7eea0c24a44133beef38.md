
## EXPLANATION (CONTINUED)

+   4 In this example, the user tries to cd to his or her home directory, but misspells home. The shell fixes the spelling and hame becomes home. The directory is changed to /home.
+   5 The output of the pwd command displays the current working directory, showing that the directory was really changed even though the user spelled it wrong.
+   6 This time the directory name is missing letters and has a misspelling for the last entry, ban. The shell makes a pretty good attempt to spell out the correct path name by inserting the missing letters, and correcting ban to man. Because the b in ban is the first misspelled character, the shell searches in the directory for an entry that might end with a and n. It finds man.
+   7 With the -u switch, shopt unsets (or turns off) the option.
+   8 With the -p switch and the name of the option, shopt indicates whether the option is set. The cdspell option has been unset (-u).

> a. The words switch and option are interchangeable. They are arguments to a command that contain a leading dash.

## 13.2.3 The Prompts

When used interactively, the shell prompts you for input. When you see the prompt, you know that you can start typing commands. The bash shell provides four prompts: the primary prompt is a dollar sign ($); the secondary prompt is a right angle bracket symbol (>); the third and fourth prompts, PS3 and PS4, respectively, will be discussed later. The prompts are displayed when the shell is running interactively. You can change these prompts.

The variable PS1 is set to a string containing the primary prompt. Its value, the dollar sign, appears when you log on and waits for user input, normally a UNIX/Linux command. The variable PS2 is the secondary prompt, initially set to the right angle bracket character (>). It appears if you have partially typed a command and then pressed Enter. You can change the primary and secondary prompts.

### The Primary Prompt.

The dollar sign (or bash $) is the default primary prompt. You can change your prompt. Normally, prompts are defined in /etc/bashrc or the user initialization file, .bash_profile, or .profile (Bourne shell).

## EXAMPLE 13.12

```
1 $ PS1="$(uname -n) > "
2 chargers >
```

## EXPLANATION

+   1 The default primary prompt is a dollar sign (bash $). The PS1 prompt is being reset to the name of the machinea (uname -n) and a > symbol.
+   2 The new prompt is displayed.

> a. The command, uname -n, is executed because it is enclosed in a set of parentheses preceded by a dollar sign. An alternative would be to enclose the command in backquotes. (See "Command Substitution" on page 835.)

## Setting the Prompt with Special Escape Sequences.

By inserting special backslash/escape sequences into the prompt string, you can customize the prompts. Table 13.2 lists the special sequences.

## Table 13.2 Prompt String Settings

| Backslash Sequence | What It Evaluates To |
|---|---|
| \d | The date in Weekday Month Date format (e.g., Tue May 26) |
| \h | The hostname |
| \n | Newline |
| \nnn | The character corresponding to the octal number nnn |
| \s | The name of the shell, the basename of $0 (the portion following the final slash) |
| \t | The current time in HH:MM:SS format |
| \u | The username of the current user |
| \w | The current working directory |
| \W | The basename of the current working directory |
| \# | The command number of this command |
| \! | The history number of this command |
| \$ | If the effective UID is 0, a #, otherwise a $ |
| \\ | Backslash |
| \[ | Begin a sequence of nonprinting characters; could be used to embed a terminal control sequence into the prompt |
| \] | End a sequence of nonprinting characters |
| New in bash 2.x+ | |
| \a | The ASCII bell character |
| \e | The ASCII escape character (033) |
| \H | The hostname |
| \T | The current time in 12-hour format: HH:MM:SS |
| \v | The version of bash, e.g., 2.03 |
| \V | The release and patchlevel of bash; e.g., 2.03.0 |
| \@ | The current time in 12-hour AM/PM format |
