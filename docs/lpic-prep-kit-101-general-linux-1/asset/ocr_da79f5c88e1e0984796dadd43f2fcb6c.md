# What Is a Shell?

This chapter presents an introduction to shells and particulars of the bash shell. It also covers input and output redirection and job control.

A shell is just another Linux program. It acts as the intermediary between the user and the operating system, and interprets what you type at the command line into a form the operating system can understand.

Table 5.1 shows some of the available shells and compares some of their features.

Table 5.1 Features of Some of the More Common Shells
| Shell | Built-In Commands | Command-Line Options |
|---|---|---|
| ash (smallest) | 24 | 10 |
| bash (Bourne Again Shell) | 48 | 12 |
| ksh (Public domain Korn Shell) | 42 | 20 |
| tcsh (emulates the csh shell) | 53 | 18 |
| zsh (one of the largest) | 84 | 50 |

By default, when you log on to your Linux computer, you are using the bash shell. Your default login shell is defined in the `/etc/passwd` file, which is covered in Chapter 7, “Users and Groups.”

The name of the shell you are using is contained in the SHELL environment variable. To verify which shell you are using, examine the value of the environment variable SHELL by typing

```
echo $SHELL
```

You also can get the same information using the finger command, as in

```
finger hadden
```

The output of the finger command has a lot of information in addition to what shell you are using, such as your home directory, your username and full name, and other personal information.

This information is defined in the contents field of the line in the `/etc/passwd` file that defines your account. You can change this information with the chfn command.

If you want to try out another shell, you can type the shell's command along with its absolute path, such as

```
/bin/csh
```