
The kill built-in sends a termination signal to a process or job. It sends the number 15 signal (termination) as mentioned in Chapter 18. The signals are the same for all three shells. The following two examples give the syntax for the kill built-in:

```
$ kill <signal> PID
$ kill -TERM %1
```

Either line will terminate a process. Remember that when you kill a process, unfinished work may be left in temporary files or permissions may be changed. A well-written program will detect and trap the arrival of signals and will clean up the tasks before exiting. Well-written applications trap the INT, QUIT, and TERM signals. Try INT with Ctrl+C. If the INT signal is ignored, then use KILL because it cannot be trapped or ignored.

The Korn shell has a whence built-in that tells you the absolute path name of a utility. The following shows its usage:

```
$ whence grep
/bin/grep
```

The whence command reports only the path names of utilities that have a path name but does not give you correct information about aliases, functions, or built-ins. If you use the -v option, it will report the type of commands or reserved words that you can use in the Korn shell. It supplies more descriptive and accurate information than whence alone. The whence built-in serves the same function as the type built-in in the Bourne and Korn shells.

The trap built-in executes a command when it receives an error or signal or upon exiting from a script or function. The syntax for trap is as follows:

```
trap '<command>' event
```

The command must be quoted because it must be passed to trap as a single argument. The event arguments are names of signals (INT, TERM) or signal numbers. This list that follows includes event arguments other than the ones mentioned in the example:

- DEBUG Occurs after every simple command. Causes your script to append the line number and the path name of the working directory to /tmp/dir_trace.
- ERR Occurs if a command exits with a nonzero status. Causes your script to execute cleanup and then exit with a status of 1.
- HUP, INT Occurs when the signal (or SIG) is received.
- EXIT or 0 Occurs whenever the script exits.

As discussed in Chapter 18, you will speed up your script writing by becoming familiar with the Korn shell’s collection of built-ins. The unique built-ins will help you solve problems not easily remedied in the other shells.

## Command-Line Editing

If you make a mistake on the current command line, the Korn shell allows you to edit the line or press the line kill key (Ctrl+K) and begin again. You can use one of the command-line editors to modify the command line. It is also possible to access and edit previous command lines stored in the history file. The Korn shell has two command-line editors. One is similar to vi and the other is similar to emacs. If you are not certain whether your Korn shell employs one or both of these, editors use one of the following four commands to check:

```
$ <visua>>vi
$ set -o vi
$ <visua>emcas
$ set -o emcas
```

### Using vi in the Korn Shell

You are in the Input mode when you type commands using vi as your command-line editor. If the visual variable is not set, the shell looks at the <editor> variable and selects an editor to use. Be sure to set the <visua> variable if you want to use vi in the Korn shell. If you discover an error in your command before you hit Return, you can switch to the vi Command mode by pressing the Esc key.

You can then use many of the vi commands to edit the command line. You can also edit previous command lines. Use the arrow keys to position the cursor if you are on a terminal that supports arrow keys. The vi editor’s positioning commands like h and I (for letters) and w and b (for words) may be preceded by a repeat factor that moves the cursor at a specified rate. (For example, 5w will move the cursor forward 5 words, and 50w will move it forward 50 words. You can specify exactly how many by putting a number before the w.) You can use the search forward or search backward commands. Use the x to delete characters or the r to replace them. The ~ will change case and . will repeat the last change. You will execute the command when you press Return. This will take effect even if you are in the middle of the command line.

When you want to edit the command line by using the full power of vi, press Esc and type v. The Korn shell will call the vi editor, but it won’t be the Korn shell’s command-line vi; it will be the full editor as described in the preceding paragraphs. When you exit with ZZ after editing with vi, the Korn shell will execute the commands you edited. In this way, you can create multiple lines of commands.

While in Command mode, you can also use several commands not found in the stand-alone vi editor. You have to set up your environment first ($ <visua>>vi) and then you can use path-name listing, path-name completion, and path-name expansion facilities to manipulate filenames.

To find a path name listing, enter Command mode and type an equal sign (=). The vi editor will respond by listing all the path names matching the current word as if an * were appended to it. The following example shows how vi reacts if you have a directory called music and you want to use cat to display one of its files but you can't remember the full name:

```
$ cat music/Br1
```

Before you press the Return key, you press the Esc key and then =. The vi command-line editor will list files and then re-echo the partial command. An example follows:

- 1) British Marching Band
- 2) Britney Spears
- 3) Brittany Travis and Company

The cursor is still on the t and you are in Command mode. Type a to append the name you are looking for.

The path-name completion facility will allow you to type a portion of a path name and vi will supply the rest. If you press the Esc key and follow it with a backslash (\), the portion of the path name that you have typed thus far may be unique enough to have vi finish it for you. If not, vi will finish it as far as it can until there are no choices to be made. The vi editor will leave you in Input mode so that you can type more. When there is no further ambiguity, the shell will append a space and leave you in Input mode.

The path-name expansion facility is much like an interactive version of file generation. To summon path-name expansion, you type a pattern followed by pressing the Esc key and an asterisk (*). This will cause the pattern to be replaced by all path names that match. The following example demonstrates how this works:

```
$ cat music/Brit
Press Esc*.
$ cat music/BritneySpears
```

If no filenames match, your terminal will flash or beep.

If Britney Spears and Brittany Travis spelled their first names alike, then path-name expansion would have listed them both. After filling in the filenames, vi will leave you in Input mode. You can continue editing or press the Return key to execute the command.

When editing, you may use the arrow keys to move about. Arrow keys work no matter which mode you are in. Table 19.8 shows the keystroke commands supported by the Korn shell.

### TABLE 19.8: THE vi COMMANDS SUPPORTED BY THE KORN SHELL

| Cursor Movement Commands | Action |
|:----------------|:-------|
| h | Moves the cursor one character to the left |
| l or spacebar | Moves the cursor one character to the right |
| w | Moves the cursor one word to the right |
| b | Moves the cursor one word to the left |
| W | Moves the cursor one space-delimited word to the right |
| B | Moves the cursor one space-delimited word to the left |
| 0 | Moves the cursor to beginning of line |
| $ | Moves the cursor to end of line |
| e | Moves the cursor to end of word |
| E | Moves the cursor to end of space-delimited word |
| `^` | Moves the cursor to first nonblank position on line |
| fx | Moves the cursor to next occurrence of x (to the right) |
| Fx | Moves the cursor to previous occurrence of x (to the left) |
| `;` | Repeats last f or F command |
| `,` | Repeats last f or F command in opposite direction |
| n`!` | Moves the cursor to column n |

| Text Editing Commands | Action |
|:----------------|:-------|
| i | Causes text editor to enter Insert mode before current character |
| a | Causes text editor to enter Insert mode after current character |
| I | Causes text editor to enter Insert mode before first nonblank character |
| A | Causes text editor to enter Insert mode at end of line |
| rx | Replaces current character with x |
| R | Overwrites text, starting at current character, until Esc is pressed |
| nx | Deletes n characters, starting at current character |
| nX | Deletes n characters, starting just past current character |
| D | Deletes from current character to end of line |
| dd | Deletes entire command |
| C | Moves the cursor from current character to end of line |
