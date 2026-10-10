# # SHELL SCRIPTS

# 23.2 Subshells

Is there any way to set up **commands** so that you can run it without explicitly invoking the shell? In other words, can you run **commands** without first typing sh, csh, or ksh? The answer is yes, but you first have to make the file *executable*. The chmod utility does this:

```
$ chmod u+x commands
```

The argument u+x tells chmod that you want to add (+) permission for the user (u) to execute (x) the shell script in the file. Now all you need do is type the file name

```
$ commands (Return)
```

and the shell will run the commands in the file.

# 23.2
Subshells

When you tell the shell to run a script such as the **commands** file, your login shell actually calls up another shell process to run the script. (**Remember,** the shell is just another program, and UNIX can run more than one program at a time.) The parent shell waits for its child to finish, then takes over and gives you a prompt:

```
$
```

Incidentally, a subshell can be different from its parent shell. For example, you can have csh or ksh as your login shell, but use sh to run your shell scripts. Many users in fact do this. When it comes time to run a script, the csh or ksh simply calls up sh as a subshell to do the job.

We will always use sh for running shell scripts. To make sure that sh is used, we will include the following line at the top of each shell script file:

```
#!/bin/sh
```

Thus, our **commands** file would look something like this:

```
#!/bin/sh
# A simple shell script
cal
date
who
```