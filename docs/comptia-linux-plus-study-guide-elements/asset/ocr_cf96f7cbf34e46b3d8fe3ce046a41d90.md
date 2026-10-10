# **TABLE 2.13** Common Environment Variables and Their Meanings

| Variable Name | Explanation |
|:-------------:|:------------|
| USER | This is your current username. It’s a variable that’s maintained by the system. |
| SHELL | This variable holds the path to the current command shell. |
| PWD | This is the present working directory. This environment variable is maintained by the system. Programs may use it to search for files when you don’t provide a complete pathname. |
| HOSTNAME | This is the current TCP/IP hostname of the computer. |
| PATH | This is an unusually important environment variable. It sets the *path*, which is a colon-delimited list of directories in which Linux searches for executable programs when you type a program name. For instance, if *PATH* is */bin:/usr/bin* and you type `1s`, Linux looks for an executable program called `1s` in */bin* and then in */usr/bin*. If the command you type isn’t on the path, Linux responds with a command not found error. The *PATH* variable is typically built up in several configuration files, such as */etc/profile* and the `.bashrc` file in the user’s home directory. |
| HOME | This variable points to your home directory. Some programs use it to help them look for configuration files or as a default location in which to store files. |
| LD_LIBRARY_PATH | A few programs use this environment variable to indicate directories in which library files may be found. It works much like *PATH*. |
| PS1 | This is the default prompt in Bash. It generally includes variables of its own, such as `\u` (for the username), `\h` (for the hostname), and `\W` (for the current working directory). This value is frequently set in */etc/profile*, but it is often overridden by users. |
| PS2 | This is the prompt for a command completion. That is, if you press the Enter key and the shell recognizes that the command is incomplete (say, because you included an open quote but not the matching close quote), the shell will present the value of this environment variable as a prompt for you to complete typing the command. |
| PAGER | Programs that use a pager typically use the pager referred to by this environment variable. It usually refers to `1ess`, but you can redefine it if you like. |
| NNTPSERVER | Some Usenet news reader programs use this environment variable to specify the name of the news server system. This value might be set in */etc/profile* or in the user’s configuration files. |