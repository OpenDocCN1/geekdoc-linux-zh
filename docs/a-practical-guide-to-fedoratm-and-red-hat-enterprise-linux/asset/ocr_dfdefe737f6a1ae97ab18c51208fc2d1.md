Next the user types c and presses <kbd>TAB</kbd> twice. The shell displays the two commands that start with `bzc`. The user types a followed by <kbd>TAB</kbd>. At this point the shell completes the command because only one command starts with `bzca`.

```
```bash
$ bzc <TAB (beep) <TAB
  bzc@at bzc@mp
$ bzca <TAB <TAB <T
```
```

# ## Pathname Completion

Pathname completion, which also uses <kbd>TAB</kbd>s, allows you to type a portion of a pathname and have bash supply the rest. If the portion of the pathname you have typed is sufficient to determine a unique pathname, bash displays that pathname. If more than one pathname would match it, bash completes the pathname up to the point where there are choices so that you can type more.

When you are entering a pathname, including a simple filename, and press <kbd>TAB</kbd>, the shell beeps (if the shell is in <u>emacs</u> mode— in <u>vi</u> mode there is no beep). It then extends the command line as far as it can.

```
```bash
$ cat films/dar <TAB (beep) cat films/dark_```

```

In the films directory every file that starts with dar has k_ as the next characters, so bash cannot extend the line further without making a choice among files. The shell leaves the cursor just past the _ character. At this point you can continue typing the pathname or press <kbd>TAB</kbd> twice. In the latter case bash beeps, displays the choices, redisplay the command line, and again leaves the cursor just after the _ character.

```
```bash
$ cat films/dark_ <TAB (beep) <TAB
  dark_passage dark_victory
$ cat films/dark_
```
```

When you add enough information to distinguish between the two possible files and press <kbd>TAB</kbd>, bash displays the unique pathname. If you enter p followed by <kbd>TAB</kbd> after the _ character, the shell completes the command line:

```
```bash
$ cat films/dark_p <TAB <T assage
```
```

Because there is no further ambiguity, the shell appends a <kbd>SPACE</kbd> so you can either finish typing the command line or press <kbd>RETURN</kbd> to execute the command. If the complete pathname is that of a directory, bash appends a slash ( / ) in place of a <kbd>SPACE</kbd>.

# ## Variable Completion

When you are typing a variable name, pressing <kbd>TAB</kbd> results in <i>variable completion</i>, wherein bash attempts to complete the name of the variable. In case of an ambiguity, pressing <kbd>TAB</kbd> twice displays a list of choices:

```
```bash
$ echo $HO <TAB (beep) <TAB
  $HOME $HOSTNAME $HOSTTYPE
$ echo $HOM <TAB <T E
```
```

# ## Pressing <kbd>RETURN</kbd> executes the command

Pressing <kbd>RETURN</kbd> causes the shell to execute the command regardless of where the cursor is on the command line.