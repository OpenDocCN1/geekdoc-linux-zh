# Executable Statements and Korn Shell Constructs.

A Korn shell program consists of a combination of UNIX/Linux commands, Korn shell commands, programming constructs, and comments.

# Naming and Storing Scripts.

When naming scripts, it is a good idea to give the script a meaningful name that does not conflict with other UNIX/Linux commands or aliases. For example, you may want to call the script test because it is merely performing some simple test procedure, but test is a built-in command and you may find yourself executing the wrong test. Additionally, if you name the file foo, goo, boobar, and so forth, in a few days or even hours you may not have any idea what is in that script!

After you have tested your script and found it bug-free, make a directory where you can store the scripts, then set the path so that your scripts can be executed from anywhere in the directory hierarchy.

# EXAMPLE 12.1

```
1  $ mkdir ~/bin
2  $ mv myscript ~/bin

(In .profile)
3  export PATH=${PATH}:~/bin
4  $ . .profile
```

# EXPLANATION

+   1. A common place to store scripts is in a directory under your home directory called bin.
+   2. The script, called myscript, is moved into the new bin directory.
+   3. The new directory is added to the PATH variable in the .profile initialization file.
+   4. The dot command causes the .profile file to be executed in the current environment so that you do not have to log out and then back in to enable the new setting.

# Making a Script Executable.

When you create a file, it is not automatically given execute permission (regardless of how umask is set). You need this permission to run your script. Use the chmod command to turn on execute permission.

# EXAMPLE 12.2

```
1  $ chmod +x myscript
2  $ ls -lF myscript
-rwxr-xr-x 1 ellie 0 Jul 12 13:00 myscript*
```

# EXPLANATION

+   1. The chmod command is used to turn on execute permission for the user, group, and others.
+   2. The output of the ls command indicates that all users have execute permission on the myscript file. The asterisk at the end of the filename also indicates that this is an executable program.