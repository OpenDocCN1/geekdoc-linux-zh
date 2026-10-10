+   - **Step** (Arrow Keys) — Press the up (↑) and down (↓) arrow keys to step through each command line in your history list to arrive at the one you want. ([Ctrl]+p and [Ctrl]+n do the same functions, respectively.)

+   - **Reverse Incremental Search** ([Ctrl]+r) — After you press these keys, you are asked to enter a search string to do a reverse search. As you type the string, a matching command line appears that you can run or edit.

+   - **Reverse Search** ([Alt]+p) — After you press these keys, you are asked to enter a string to do a reverse search. Type a string and press [Enter] to see the most recent command line that includes that string.

+   - **Forward Search** ([Alt]+n) — After you press these keys, you are asked to enter a string to do a forward search. Type a string and press [Enter] to see the most recent command line that includes that string.

+   - **Beginning of History List** ([Alt]+←) — Brings you to the first entry of the history list.

+   - **End of History List** ([Alt]+→) — Brings you to the last entry of the history list.

Another way to work with your history list is to use the `fc` command. Type `fe` followed by a history line number, and that command line is opened in a text editor. Make the changes that you want. When you exit the editor, the command runs. You can also give a range of line numbers (e.g., `fc 100 105`). All the commands open in your text editor and then run one after the other when you exit the editor.

The history list is stored in the `.bash_history` file in your home directory. Up to 1,000 history commands are stored for you by default. Not that this does serve as a history of your commands, something the root or other users may not want to expose.

# ## Connecting and Expanding Commands

A truly powerful feature of the shell is the capability to re-direct the input and output of commands to and from other commands and files. To allow commands to be strung together, the shell uses metacharacters. As noted earlier, a *metacharacter* is a typed character that has special meaning to the shell for connecting commands or requesting expansion.

# ### Piping Commands

The `pipe` (|) metacharacter connects the output from one command to the input of another command. This lets you have one command work on some data, and then have the next command deal with the results. Here is an example of a command line that includes pipes:

```
```
$ cat /etc/passwd | sort | cut -f,5 -d : | less
```
```

This command lists the contents of the `/etc/passwd` file and pipes the output to the `sort` command. The `sort` command takes the usernames that begin each line of the `/etc/passwd` file, sorts them alphabetically, and pipes the output to the `cut` command. The `cut` command takes fields 1 and 5, with the fields delimited by a colon (:), then pipes the output to the `less` command.