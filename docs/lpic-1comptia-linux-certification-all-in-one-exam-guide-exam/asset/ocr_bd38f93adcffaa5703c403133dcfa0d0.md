| Environment Variable | Stores | Default Value |
| :--- | :--- | :--- |
| BASH and SHELL | The full path to the shell executable | /bin/bash |
| CPU | The type of CPU installed in the system | Depends on your system. An Intel Pentium IV computer would have a value of i686 |
| DISPLAY | The location where your X Window display should be sent | 0.0 (the local video card and monitor) |
| ENV | The name of the file bash read to configure its environment | /etc/bash.bashrc |
| EUID | The user ID (UID) of the current user | The UID number of the current user |
| HISTFILE | The path to the bash command history file | ~/bash_history |
| HISTSIZE | The number of commands saved in the command history file | 1000 |
| HOME | The path to the current user's home directory. | The current user's home directory |
| HOST and HOSTNAME | The hostname of the system | The hostname you assigned when you installed the system |
| LOGNAME | The username of the current user | The username of the current user |
| MAIL | The path to the current user's mailbox file | /var/spool/mail/username or /var/mail/username |
| MANPATH | The path to your system's man program | Depends on the distribution |
| OLDPWD | The path to the prior current directory | Depends on what your prior current directory was |
| OSTYPE | The type of operating system currently being run | Linux |
| PATH | A list of directories to be searched when running a command from the shell prompt | Depends on your distribution |
| PS1 | The characters used to create the shell prompt | Depends on your distribution |
| PWD | The path to the current working directory | Depends on what your current directory is |

Table 2-5 Commonly Used Environment Variables

# Viewing Variables and Their Values

If you need to see the value assigned to a variable on your system, you can use a variety of different commands from the shell prompt. If you need to see the value of a single variable, you can use the echo command. The syntax is *echo variable*. For example, if I wanted to view the value of the PATH variable, I would enter *echo $PATH* at the shell prompt. This is shown in Figure 2-19.