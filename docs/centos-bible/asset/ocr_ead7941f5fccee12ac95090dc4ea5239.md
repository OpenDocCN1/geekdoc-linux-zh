# Part I

# Getting Started

Linux: To avoid getting logged off while you are working, you may want to set the value to something like $TMOUT=1800 (to allow 30 minutes of idle time), or simply do not set this variable to disable this feature.

+   PATH — As described earlier, the $PATH variable sets the directories that are searched for commands you use. If you often use directories of commands that are not in your PATH, you can permanently add them. To do this, add a $PATH variable to your .bashrc file. For example, to add a directory called /example/bin, add the following:

```
PATH=$PATH:/example/bin ; export PATH
```

+   This example first reads all the current directory directories into the new PATH ($PATH), adds the /example/bin directory, and then exports the new PATH.

![](bbox=[0.05, 0.34, 0.2, 0.38])

> Some people add the current directory to their PATH by adding a directory identified simply as a dot (.), as follows:

```
PATH=.:$PATH ; export PATH
```

This lets you always run commands in your current directory. However, the security risk with this procedure is that you could be in a directory that contains a command that you don't intend to run from that directory. For example, a malicious person could put an ls command in a directory that, instead of listing the content of your directory, does something devious.

+   WHATEVER — You can create your own environment variables to provide shortcuts in your work. Choose any name that is not being used and assign a useful value to it. For example, if you do a lot of work with files in the /work/time/files/info/memos directory, you could set the following variable:

```
M=/work/time/files/info/memos ; export M
```

+   You can make that your current directory by typing cd $M. You can run a program called reminder from that directory by typing $M/reminder. You can edit a file called cellphone_policy.txt from there by typing vi $M/cellphone_policy.txt.

# Adding Aliases

Setting aliases can save you even more typing than setting environment variables. With aliases, you can have a string of characters execute an entire command line. You can add and list aliases with the alias command. Here are some examples:

```
alias p='pwd ; ls -CF'
alias r='rm -i'
```

In the first example, the letter p is assigned to run the command pwd, and then to run ls -CF to print the current working directory and list its contents in column form. The second runs the rm command with the -i option each time you simply type rm. This is an alias that is set by default in CentOS for the root user, so that instead of just removing files, you are prompted for