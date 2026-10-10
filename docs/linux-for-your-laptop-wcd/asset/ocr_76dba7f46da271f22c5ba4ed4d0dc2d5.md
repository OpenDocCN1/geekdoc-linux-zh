| Table 9.1 Common Bash Shell Variables |
|---|---|
| **Variable** | **Description** |
| BASH_ENV= | Your shell's resource file |
| EDITOR= | The default system text editor |
| HISTSIZE= | The number of lines available for history use |
| HOME= | Your home directory |
| HOSTNAME= | The hostname of your notebook |
| HOSTTYPE= | The type of computer in use |
| LOGNAME= | Your login name |
| MACHINE= | The type of system you're using |
| MAIL= | Your system mail directory |
| NNTPSERVER= | The hostname of your ISP's Usenet news server |
| OSTYPE= | The operating system in use |
| PATH= | Recognized directories containing executable programs |
| PS1= | The definition of your shell prompt |
| PWD= | The current working directory |
| SHELL= | The current shell in use |
| TERM= | If you're using X11, the type of terminal running the shell |
| USER= | The current user's username |

In this example, the output of the `1s` command is redirected to a file. You can also use input and output redirection at the same time to create a simple text editor with the `cat` command:

```
```
$ cat >myfile.txt <<.
> This is the most easy to use editor
> available for Linux, and will quickly
> create a short text file.
> .
```
```

In this example, the `cat` command is instructed to send its output to the file myfile.txt, and the redirection here (`<<.`) operator is used to specify an end-of-file marker. After pressing Enter, you can type and press Enter to create a text file.