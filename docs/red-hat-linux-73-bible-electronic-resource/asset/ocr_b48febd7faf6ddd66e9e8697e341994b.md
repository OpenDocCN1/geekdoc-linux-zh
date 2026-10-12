+   BASH_VERSION — A number that represents the current version of the bash command.

+   BASH_ENV — This value identifies the location of a file that contains commands used to initialize the shell. For the bash shell, this file is probably $HOME/.bashrc. See the section about creating configuration files for information on working with the .bashrc file.

+   EUID — This is the effective user ID number of the current user. It is assigned when the shell starts, based on the user’s entry in the /etc/passwd file.

+   FCEDIT — If set, this indicates the text editor used by the fc command to edit history commands. If this variable isn’t set, the vi command is used.

+   HISTFILE — The location of your history file. It is typically located at $HOME/.bash_history.

+   HISTFILESIZE — The number of history entries that can be stored. After this number is reached, the oldest commands are discarded. The default value is 1000.

+   HISTCMD — This returns the number of the current command in the history list.

+   HOME — This is your home directory. It is your current working directory each time you log in or type the cd command with no options.

+   HOSTTYPE — A value that describes the computer architecture on which the Linux system is running. For Intel-compatible PCs, the value is i386, i486, i586, or i686.

+   MAIL — This is the location of your mailbox file. The file is typically your user name in the /var/spool/mail directory.

+   OLDPWD — The directory that was the working directory before you changed to the current working directory.

+   OSTYPE — A name identifying the current operating system. In our case, this will say linux-gnu. (Bash can run on other operating systems as well.)

+   PATH — The colon-separated list of directories used to find commands that you type. This value is initially set by the operating system, although most people modify it. The default value for regular users is:

```
/bin:/usr/bin:/usr/local/bin:/usr/bin/X11:/usr/X11R6/bin:~/bin
```

For the root user, the value also includes /sbin, /usr/sbin, and /usr/local/sbin.

+   PPID — The process ID of the command that started the current shell (for example, its parent process).

+   PROMPT_COMMAND — Can be set to a command name that is run each time before your shell prompt is displayed. Setting PROMPT_COMMAND=date prints the current date and time before the prompt line appears.

+   PS1 — Sets the value of your shell prompt. There are many items that you can read into your prompt (date, time, user name, host name, and so on). Sometimes a command