
The zsh shell executes these files immediately after the startup files when starting an interactive shell:

```
% zsh
This is the /etc/zshenv file.
This is the .zshenv file in HOME.
This is the /etc/zshrc file.
This is the .zshrc file in HOME.
%
```

Since a login shell is also an interactive shell, the zsh shell executes the contents of the zshrc files as well:

```
% zsh -l
This is the /etc/zshenv file.
This is the .zshenv file in HOME.
This is the /etc/zprofile file.
This is the .zprofile file in HOME.
This is the /etc/zshrc file.
This is the .zshrc file in HOME.
This is the /etc/zlogin file.
This is the .zlogin file in HOME.
%
```

Notice the order in which the zsh shell executes the files. The zshrc file pair is executed after the zprofile files, but before the zlogin files.

### The shell logout files

Besides the login and startup files, the zsh shell also has the ability to execute commands in files when you log out from an interactive or login shell session. These files can be in the following locations:

- /etc/zlogout
- $HOME/.zlogout

As you probably figured out by now, every user on the system executes the commands in the /etc/zlogout file at logout, while each individual user has a unique $HOME/.zlogout file.

The zsh shell will execute any commands in these files before logging out of the current shell. This doesn't include just exiting from an interactive shell. Thus, if you just start another zsh shell from an existing shell session, the zsh shell won't execute the logout files when you exit the shell. However, if you start a login shell, the logout files should execute upon exiting:

```
% zsh -l
This is the /etc/zshenv file.
This is the .zshenv file in HOME.
This is the /etc/zprofile file.
This is the .zprofile file in HOME.
This is the /etc/zshrc file.
This is the .zshrc file in HOME.
This is the /etc/zlogin file.
This is the .zlogin file in HOME.
$ exit
This is the .zlogout file in HOME.
This is the /etc/zlogout file.
$
```

Notice that the shell executes the `.zlogout` file before the global `zlogout` file, which is in the opposite order from the other zsh file types.

## Part IV: Working with Alternative Shells

### Environment variables

Just like any other shell, the zsh provides standard environment variables for tracking system and shell information. The zsh uses a combination of lowercase variable names and uppercase variable names.

There are a few environment variables for which the zsh shell provides both a lowercase and uppercase version. The reason for this is in the way the zsh handles arrays, and compatibility with other shells.

The zsh shell uses a space-separated list of words to define an array. Many Bourne shell-derived shells use a colon to separate array elements in multi-value variables, such as the `PATH` variable in the Bash shell.

To maintain compatibility, the zsh shell provides a lowercase `path` variable, which uses the zsh-style array, and an uppercase `PATH` variable, which uses the Bourne-style array. Table 23.2 lists the environment variables found in the zsh shell.

**TABLE 23.2 The zsh Environment Variables**

| Variable | Description |
| :--- | :--- |
| `!` | The process ID of the last background command. |
| `#` | The number of parameters specified on the command line. |
| `$` | The process ID of the shell. |
| `*` | An array containing the command line positional parameters. |
| `-` | Options set on the command line. |
| `argv` | An array containing the command line positional parameters. |
| `ARGV0` | The value of argv[0] of external commands, which is usually the command name. |
| `BAUD` | The baud rate of the current connection. |
| `cdpath` | An array of directories used for the search path in the cd command. |
| `CDPATH` | The same as cdpath, but using a colon as the field separator. |
| `COLUMNS` | The number of columns in the terminal session. |
| `CPUTYPE` | The microprocessor class or model of the system. |
| `DIRSTACKSIZE` | The maximum size of the directory stack. |
| `EGID` | The effective group ID of the shell process. |
| `ENV` | If the shell is invoked as a Bourne or Korn shell, this variable contains the location of the `zprofile` file. |
| `ERRNO` | The error status of the most recently failed system call. |
| `EUID` | The effective user ID of the shell process. |
| `FCEDIT` | The default editor used in the command history editor. |
| `fignore` | An array of file suffixes to ignore during file completion. |
| `FIGNORE` | The same as `fignore`, but using a colon as the field separator. |
| `fpath` | An array of directories specifying the search path for functions. |
| `FPATH` | The same as `fpath`, but using a colon as the field separator. |
| `GID` | The real group ID of the shell process. |
| `histchars` | Characters used by the history command. |
| `HISTCMD` | The current history line number. |
| `HISTFILE` | The file to save the history in when exiting an interactive shell. |
| `HISTSIZE` | The maximum number of events allowed in the history file. |
| `HOME` | The user's default working directory. |
| `HOST` | The current hostname. |
| `IFS` | The internal file separators, defaults to space, tab, newline, and the `NUL` character. |
| `KEYTIMEOUT` | The time the shell waits (in hundredths of a second) for another key to be pressed when reading multi-character sequences. |
| `LANG` | The locale category for any category not covered by a LC variable. |
| `LC_ALL` | The locale category that overrides all other defined locale categories. |
| `LC_COLLATE` | The locale category used to determine character collision. |
| `LC_CTYPE` | The locale category used to determine character handling functions. |
| `LC_MESSAGES` | The locale category used to display messages. |
| `LC_NUMERIC` | The locale category used to display decimal point and thousands separator characters. |
| `LC_TIME` | The locale category used to display dates and time. |
| `LINES` | The number of lines in the terminal session. |
| `LINENO` | The line number of the current command in the script or shell function. |
| `LISTMAX` | The number of matches to list in the line editor before asking for more. |
| `LOGCHECK` | The interval in seconds between checking for inactivity using the watch parameter. |
| `LOGNAME` | The login name corresponding to the current shell session. |
| `MAIL` | If set the shell checks for mail in the specified file. |
| `MAILCHECK` | The interval in seconds between mail checks. |
| `mailpath` | An array of filenames to check for mail. |
| `MAILPATH` | The same as `mailpath`, but using a colon as the field separator. |
| `manpath` | An array of directories not used by the `zsh` shell (relates to `MANPATH` used in the Bourne shell). |
| `MANPATH` | The same as `manpath`, but using a colon as the field separator. |
| `module_path` | An array of directories used by `zmodload` to load new `zsh` modules. |
| `MODULE_PATH` | The same as `module_path`, but using a colon as the field separator. |
| `NULLCMD` | The command name to assume if a redirection is specified with no command. The default is the `cat` command. |
| `path` | An array of directories to search for commands. |
| `PATH` | The same as `path`, but using a colon as the field separator. |
| `POSTEDIT` | A string to display whenever exiting the line editor. |
| `prompt` | The primary prompt string used by the shell. |
| `PROMPT` | The same as `prompt`. |
| `PROMPT2` | The secondary prompt string used when more input is required for a command. |
| `PROMPT3` | The selection prompt used in a select loop. |
| `PROMPT4` | The trace prompt used when tracing a command. |
| `PS1` | The same as `PROMPT`. |
| `PS2` | The same as `PROMPT2`. |
| `PS3` | The same as `PROMPT3`. |
| `PS4` | The same as `PROMPT4`. |
| `psvar` | An array whose first nine values are referenced by the associated prompt strings. |
| `PSVAR` | The same as `psvar`, but using a colon as the field separator. |
| `RANDOM` | A random number generator for integers between `0` and `32767`. |
| `READNULLCMD` | The default command name if an input redirection is specified with no command. The default is the `more` command. |
| `REPORTTIME` | Array of commands to report timing statistics for. |
