
## Command completion

The bash shell includes a feature called command completion. This enables you to type the first few letters of the command at the prompt, hit the Tab key, and have the system complete the command for you. If you wish to run the command `dmesg` to display the kernel ring buffer, you could type the following:

```bash
$ dm
```

If you then hit the Tab key, the system will fill in the following command:

```bash
$ dmesg
```

If there is more than one possible match to what you typed before pressing the Tab key, the system will simply beep. Pressing the Tab key once again will display all of the possible command matches. Pressing the Esc twice performs the same action as pressing the Tab key.

### Editing commands with the Readline Library

The bash shell allows you to edit commands you type at the shell prompt before pressing the Enter key. The editor used for editing these commands is the Readline Library. This editor runs by default in the emacs mode using the same keystrokes as the emacs editor. The Readline Library enables you to easily fix errors in your command sequence without having to retype the entire sequence. You can easily move your cursor to the spot where you want to make changes and either delete or insert the corrections into the command line. When the error has been fixed you can simply press Enter without moving to the end of the line. The special keys used by the Readline Library and their functions are listed in Table 2-3. While this information is not required for the exam, it can be very useful when working with the command line.

Table 2-3
Readline Library Commands

| Key Combination | Function |
| --- | --- |
| Ctrl-b | Move back one character. |
| Ctrl-f | Move forward one character. |
| Del | Delete the character to the left of the cursor. |
| Ctrl-d | Delete the character underneath the cursor. |
| Ctrl-a | Move to the start of the line. |
| Ctrl-e | Move to the end of the line. |
| Esc-f | Move forward a word. |
| Esc-b | Move backward a word. |
| Ctrl-l | Clear the screen, reprinting the current line at the top. |
| Ctrl-k | Kill (delete) the text from the current cursor position to the end of the line. |
| Esc-d | Kill from the cursor to the end of the current word, or if between words, to the end of the next word. |
| Esc-Del | Kill from the cursor the start of the previous word, or if between words, to the start of the previous word. |
| Ctrl-w | Kill from the cursor to the previous white space. This differs from Esc-Del because the boundaries separating words differ. |

The editor can be configured globally using the `/etc/inputrc` file for global changes. To make changes for a specific user you can edit the `.inputrc` file located in the user’s home directory. This file can be used to change the key mappings for the Readline Library editor, and map keys to commonly used commands. To view your keyboard bindings type the following command:

```bash
$ bind -v
```

## Command substitution

It is possible to replace a command with the output it produces. This is known as command substitution. Command substitution is a valuable tool used with scripts. This allows the output from one command to work as the argument for another. A useful example of this is the `pwd` command. The `echo` command is used to output the `pwd` so that it is available to the system.

```bash
# echo $(pwd)
```

## Using the history file

- **Work effectively on the UNIX Command Line.** Includes using command history and editing facilities.

The history file contains a list of the commands issued at the command prompt. The number of commands stored here is specified by the `HISTSIZE` environment variable in either the /etc/profile or ~/.profile file. The default setting for this variable is 1,000 entries. The `history` command displays all entries in the history file, which is ~/.bash_history.

You can cycle through the entries in the history file the arrow keys. The up arrow will cycle to previous entries in the command history while the down arrow cycles down through the command history. This can provide a shortcut to running commands that you entered earlier. When cycling through the commands, you can edit them on the command line before rerunning the commands.

The `HISTCMD` variable is used to provide the history index number of the command currently being run. The `HISTFILE` variable specifies the file used to contain the command history, with the default of /home/user/.bash_history. The `HISTFILESIZE` variable specifies the maximum number of lines contained in the HISTFILE.

### `fc`

The `fc` utility provides another option for editing commands in the history file before running them. The `fc` utility opens the command into the default editor, where you can edit and save it before rerunning the command. The `fc` utility allows you to specify the number of the history events to edit, which enables you to edit a range of commands at once. The editor to use can also be specified using this command. Once the editor is invoked using the `fc` command the file is processed like any other text file using the editor. For instance, the `-l` option is used to list a range of values. The following example uses the `fc` utility to list the history events 1020-1025.

```bash
$ fc -l 1020 1025
 1020  cd /etc
 1021  ls -al
 1022  vi services
 1023  vi hosts
 1024  man ls
 1025  ls -al s*
```

## Environment Variables and Settings

**Objective** 1.3 GNU and UNIX Commands

- *Work effectively on the UNIX Command Line. Includes defining, referencing and exporting environment variables.*
