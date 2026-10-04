As you can see, when the shell script is run, the parameter (/etc) is substituted into the ls command in the pipeline, in place of the $1. This substitution is done by the shell and the ls command has no idea that it has taken place.

In order that you can access this new command wherever you are in the directory hierarchy, you need to make sure that the directory which contains the command is listed in your PATH variable. The next example creates a bin directory under your home directory, moves the dirsize command into it and adds this bin directory to the start of your PATH so that the directory will be searched automatically by the shell whenever you enter a command name. The value of the shell variable HOME is used in the example, as it contains the pathname of your home directory:

```
$ echo $PATH
/bin:/usr/bin:.
$ mkdir $HOME/bin
$ mv dirsize $HOME/bin
$ PATH=$HOME/bin:$PATH
$ echo $PATH
/usr1/pc/bin:/bin:/usr/bin:.
```

Remember that the list of directories contained in the PATH variable are separated by colons. The initial contents of PATH show that three directories will be searched for any commands you enter: /bin first, then /usr/bin and, finally, dot, the current directory. The command sequence then modifies the value of PATH by adding /usr1/pc/bin: onto the front of the PATH, so that this directory is searched before the other three, whenever a command is entered.

An alternative notation which you can use when you want to refer to your home directory, in place of $HOME, is to use the tilde (~) symbol. Using this notation $HOME/bin is the same as ~/bin. The tilde notation can also be extended by following it with the login name of another user. In this case the notation expands to be the pathname of the home directory of the specified user. For example:

```
$ ls ~carey/bin
```

would list the contents of bin under the home directory of user carey, assuming that I have permission to read the contents of this directory.

# 6.4 Login Scripts

Performing actions like changing your PS1 shell prompt can be quite fun. And adding personal extras to the contents of PATH can be very useful. However, when you have to perform these actions every time you login before they will take effect, it can soon become quite tedious.

The solution to this problem is to create a personal login script which the shell will automatically read and execute for you when you login. A personal login script