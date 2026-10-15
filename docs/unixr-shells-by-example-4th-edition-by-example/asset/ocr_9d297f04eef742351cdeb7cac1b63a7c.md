# Executable Statements and Bourne Shell Constructs.

A Bourne shell program consists of a combination of UNIX commands, Bourne shell commands, programming constructs, and comments.

# Making the Script Executable.

When you create a file, it is not given the execute permission. You need this permission to run your script. Use the chmod command to turn on the execute permission.

# EXAMPLE 8.1

```
1  $ chmod +x myscript
2  $ ls -lF myscript
-rwxr-xr-x  1 ellie  0 Jul 13:00 myscript*
```

# EXPLANATION

+   1 The chmod command is used to turn on the execute permission for the user, group, and others.
+   2 The output of the ls command indicates that all users have execute permission on the myscript file. The asterisk at the end of the filename also indicates that this is an executable program.

# A Scripting Session.

In the following example, the user creates a script in the editor. After saving the file, the execute permissions are turned on, and the script is executed. If there are errors in the program, the shell will respond immediately.

# EXAMPLE 8.2

```
(The Script)
1  #!/bin/sh
2  # Scriptname: greetings
# Written by: Barbara Born
# This is the first Bourne shell program of the day.
3  echo "Hello $LOGNAME, it's nice talking to you."
4  echo "Your present working directory is `pwd`."
   echo "You are working on a machine called `uname -n`."
   echo "Here is a list of your files."
5  ls      # List files in the present working directory
6  echo "Bye for now $LOGNAME. The time is `date +%T`!"

(The Command Line)
7  $ chmod +x greetings
   $ greetings
3  Hello barbara, it's nice talking to you.
```