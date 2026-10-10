# **Part II: Shell Scripting Basics**

If you entered this code, congratulations, you just wrote a shell script! This simple script uses just two Bash shell commands. The date command runs first, displaying the current date and time, followed by the output of the who command, showing who is currently logged on to the system. Using this technique, you can string together as many commands as you want, up to the maximum command-line character count of 255 characters.

Although using this technique is fine for small scripts, it has a major drawback in that you have to enter the entire command at the command prompt every time you want to run it. Instead of having to manually enter the commands on a command line, you can combine them into a simple text file. When you need to run the commands, you just simply run the text file.

# # Creating a Script File

To place shell commands in a text file, first you'll need to use a text editor (see Chapter 10, “Working with Editors”) to create a file and then enter the commands into the file.

When creating a shell script file, you should specify the shell you are using in the first line of the file. The format for this is

```
#!/bin/bash
```

In a normal shell script line, the pound sign (#) is used as a comment line. A comment line in a shell script isn’t processed by the shell. (However, the first line of a shell script file is a special case, and the pound sign followed by the exclamation point tells the shell what shell to run the script under (yes, you can be using a Bash shell and run your script using another shell)).

After you indicate the shell, commands are entered onto each line of the file, followed by a carriage return. As mentioned, comments can be added by using the pound sign. An example looks like this:

```
#!/bin/bash
# This script displays the date and who's logged on
date
who
```

And that’s all there is to it. You can use the semicolon and put both commands on the same line if you want to, but in a shell script, you can list commands on separate lines. The shell will process commands in the order in which they appear in the file.

Also notice that another line was included that starts with the pound symbol and adds a comment. Lines that start with the pound symbol (other than the first #! line) aren’t interpreted by the shell. This is a great way to leave comments for yourself (and others) about what’s happening in the script so that when you come back to it two years later you can easily remember what you did.

Save this script in a file called test1, and you are almost ready. There are still a couple of things to do before you can run your new shell script file.

If you try running the file now, you’ll be somewhat disappointed to see this: