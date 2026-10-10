Normal users will have two similar files, which are also called as

+   *   `/home/user/.bash_profile` This is a personal startup file and is executed when a user logs into a system.

+   *   `/home/usr/.bashrc` This is the personal interactive shell startup file.

Both the above files can be edited by the user using an editor such as vi. The format for creating and modifying an environment variable within bash is always in the format given below:

```
NAME=value
```

This will define the variable in the shell only. To move that from the shell to the environment, the `export` command has to be used:

```
export  NAME=value
```

This allows programs other than the shell to access this variable (for instance, a file editor).

# PS1

When a user first logs on, they will be greeted by a prompt. This prompt can be changed and may be different depending on the version of Linux that has been installed. The typical prompt for a standard user is the `$` symbol, while root is denoted by the `#` symbol. This can be demonstrated below (user input is in boldface).

```
$ who am i
syngress
$ su root
Enter password for root: xxxxxx
# who am i
root
# exit
$ who am i
Syngress
```

The user prompt defined initially in the file `/etc/bash.bashrc` as the environment variable PS1 can display a vast array of data. The PS1 variable can change the command line as shown below:

```
$ PS1="\u>"
syngress>
```

Typical variables that are used are given below:

`\d` is the date in “Wed Sep 09” format