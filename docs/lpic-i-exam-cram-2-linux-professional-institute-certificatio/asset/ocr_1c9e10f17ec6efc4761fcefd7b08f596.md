The `11` alias substitutes for the `1s -1` command, making long listings much easier; the `1d` alias, on the other hand, shows a directory entry's long listing, not the contents of the directory. Finally, the `1f` alias helps you determine the file type on terminals that don't support color.

> **ALERT**
> Watch for questions about aliases, such as `11` and `1f`, or how to create them.

The `1s` command's `-f` option supports suffixing entries with various characters that denote the file type:

+   - `/-`—Directory entries are suffixed with a forward slash, such as `etc/`.
+   - `*`—Executable files are suffixed with an asterisk, such as `scriptfile*`.
+   - `e`—Symbolic links are suffixed with an `e` symbol, such as `rc.de`.
+   - `=—`—Sockets are suffixed with an equal symbol, such as `gpmtcl-`.
+   - `|`—Fifos or pipes are suffixed with a `|` symbol, such as `inotetl|`.

> **NOTE**
> It's only after you have pressed the Enter key that your command string is checked for the presence of matching words to the aliases defined in your shell. If you try to get too tricky with an alias, you'll either get an error or end up creating or deleting things you need. For more complex tasks, see the section "Shell Functions."

> **ALERT**
> Watch for questions that test you on troubleshooting nonfunctional or circular alias commands and aliases that are defined for common commands. Also, watch for questions about how to cause an alias to be ignored.

# # Shell Functions

A *shell function* incorporates the functionality of shell aliases and includes the capability to recursively perform tasks, break tasks up into chunks that are more readable, and in general perform the same functionality as a script but from memory rather than from disk.

A function incorporates all the capabilities of an alias and adds the capability to be recursive or perform loop iterations and arguments to the commands in a function.

Functions are executed at the same level or in the current shell. No new shells are used, allowing the function full access to the shell's variables and settings.