
can also delete text from the command line by using the **Backspace** or **Delete** keys. Most users should find these simple editing commands sufficient, but, for those who do not, `tcsh` also supports a wide range of equivalent `emacs` and `vi` editing commands.

Another method of using the history file is to display and edit the history list using a number of other editing commands that `tcsh` provides. The **history** command can be invoked by any one of three different methods.

First, the history list may be displayed to the screen as follows:

```
history [-nr] [n]
```

- The **n** option is used to specify the number of commands to display. If the **n** option is not used, the **history** command will display the entire history list.
- The **-n** option causes **history** to remove the command numbers and timestamps that are usually present in the output of the **history** command.
- The **-r** option tells **history** to display the commands in reverse order, starting with the most recent command.

Second, the contents of the history file or the history list may be modified as follows:

```
history -S |-L |-M [filename]
```

- The **-S** option writes the history list to a file.
- The **-L** option appends a history file to the current history list.
- The **-M** option merges the contents of the history file with the current history list and sorts the resulting list by the timestamp contained with each command.

![](img/df365d352a104b50fea29e59a052de4d_111_0.png)

> All the options for the second form of the **history** command use the `filename` option as the name of the history file. If no `filename` is specified, the **history** command will use the `value` of the `histfile` variable. If the `histfile` variable isn't set, it will use the `~/.history` (home directory) file.

Third, the current history list may be cleared with this command:

```
history -c
```

In addition to the **history** command and its options, `tcsh` also contains many history navigation and editing commands. The following commands are used to navigate through the history list:

- **!n**: Reexecutes the command with the history number of n.
- **!-n**: Reexecutes the command that is n commands from the end of the history list.
- **!!**: Reexecutes the last command that was entered.
- **!c**: Reexecutes the last command in the history list that begins with the letter c.
- **!?c?**: Reexecutes the last command in the history list that contains the letter c.

The history editing commands allow you to replace words and letters in previously entered commands, as well as to add words to the ends of previously entered commands. More information on these editing commands can be found by referring to the tcsh man page.

## tcsh Command Completion

Just like bash, tcsh command-line completion may be invoked by pressing the Tab key at any point while typing a command.

When you press the Tab key, tcsh tries to complete the command by matching what has been typed with any file in the directory to which the command is referring. For example, assume that you typed the following command and then pressed the Tab key:

```
emacs hello
```

Here, tcsh will try to match the letters in hello with any file (or subdirectory) in the current directory. If there is a simple file in the current directory that begins with the letters hello, tcsh fills in the rest of the filename for you. Now assume that you typed the following command and then pressed the Tab key:

```
emacs /usr/bin/hello
```

In this case, tcsh would try to match the letters hello with any file in the /usr/bin/ directory. From these examples, you can see that you must give tcsh something to go on before asking it to complete the command for you.

Here is another example of using command-line completion. Assume that the directory you are currently in contains these files:

```
News/  bin/  mail/  sample.txt  testfile  ttd.txt
```

If you want to print the sample.txt file, you could type the following command:

```
lpr sample.txt
```

Using command-line completion, you could get away with typing the following command and then pressing the Tab key:

```
lpr s
```

At this point, *tcsh* attempts to complete the command and finds that the only file that can possibly match what was typed so far is the *sample.txt* file. *tcsh* would then complete the command by putting the following text on the command line:

```
lpr sample.txt
```

You can now either confirm that this is the intended command by pressing the Enter key, or you can edit the command if it isn’t what you intended.

## tcsh Variables

Following are some of the most useful *tcsh* variables:

- **autocorrect**: If this is set, *tcsh* will automatically try to correct command-line spelling errors.
- **histfile**: The name of the file that is used to store the command history.
- **history**: The size of the history list.
- **home**: The user’s home directory.
- **path**: The search *path* that *tcsh* uses when looking for executable programs.
- **prompt**: The first-level prompt that is displayed on the command line.
- **prompt2**: The second-level prompt that is displayed when a *for*, *foreach*, or *while* loop is expecting input.
- **prompt3**: The third-level prompt that is displayed when *tcsh* has attempted to correct a spelling error in a command.
- **savelist**: This variable must be set to the number of history commands that you want to save, if you want *tcsh* to save the history list when you log out.
- **watch**: Contains a list of user terminal pairs to watch for logins and logouts.

These variables are used to customize *tcsh* for each user and are explored in the section on configuration files.

## tcsh Configuration Files

Many of the *tcsh* variables may be used at the command line to change the way *tcsh* operates for a single session. For the changes to apply to all future sessions, however, they must be saved to a file that is executed each time you start *tcsh*.

Several initialization files are important to *tcsh*. The commands in these files are executed when you first log in.

For a login to a standard installation of *tcsh*, configuration files would be sourced in this order:

- `/etc/csh.cshrc`: The commands in this file are executed each time a copy of the *tcsh* program is run. Examples of the types of commands that usually appear in this file are aliases and variable declarations.
- `/etc/csh.login`: Normally, to change any of the settings found in *csh.login*, you would copy it to your home directory as `~/.login` and make the changes you want there.
- `~/tcshrc` or `~/cshrc`: *tcsh* next sources any copy of the `.cshrc` file in your home directory.
- `~/.history`: The history file is brought in next.
- `~/.login`: Your personal login file in your home directory (if you have created one) follows.
- `~/.cshdirs`: Finally, *tcsh* checks your home directory for this file, which loads the directory stack.

For a normal non-login shell, startup would occur as follows:

`/etc/csh.cshrc` --> `~/.tcshrc` (or `~/cshrc`)

In OpenLinux, however, the *tcsh* startup process is considerably more complex. The file `/etc/csh.cshrc` is sourced first, followed by `~/.tcshrc` which pulls in `/etc/config.d/shells/csh.cshrc`. This additional layer of configuration is unique to OpenLinux, which then sources:

- `~/.tcshrc-all`: The individual user’s *tcsh* defaults; however, if this file is not available, it uses `~/cshrc-all` for the individual user’s *tcsh* defaults.
- `~/.tcshrc-interactive`: The individual user’s *tcsh* interactive shell defaults, or, if this file is not available, `~/cshrc-interactive`.
- `~/.history`: The user's command history.
- `~/.login`: The individual user's generic login settings. It pulls in `/etc/config.d/shells/csh.login` for the system login defaults.
- `~/.login-private`: Which is the individual user's *tcsh* login settings.

## Summary

In this chapter, we studied the basic configuration and usage of two popular shells, **bash** and **tcsh**. The commands detailed in this chapter will get you started working in a shell.

Either of these two shells is admirably suited for everyday use of your OpenLinux system, and your choice between the two will depend on your individual preference and usage patterns.
