your command history. You can do so line by line by pressing the up\-arrow key repeatedly until you locate the command you want to re\-execute. Then just press the Enter key to run the command again.

![](bbox=[0.16, 0.15, 0.23, 0.24])

> The `history` command lists your last 20 commands (by default) when you enter it at the prompt, in case you’re curious about what they were. If you want to see a longer list of them, use the techniques covered in Chapter 11 to view the contents of the file `~/.bash_history`.

# Working with Variables

*Variables* in the bash shell are words or strings of text that computers use to represent a piece of data. An example of using a variable is setting the variable `fruit` to contain the text `apple`. A number of standard variables contain information about your account and environment settings.

# Variables versus environment variables

The first thing I need to make clear is that the bash shell has two types of variables:

+   \- *Variables*: A variable can be referenced in a program or shell session, but it’s visible and available to only that session or program.
+   \- *Environment variables*: An environment variable can also be referenced by the shell or program. However, it has the added behavior of having its value copied to any other program or shell that is created from its environment.

![](bbox=[0.16, 0.65, 0.23, 0.73])

You can usually tell at a glance the difference between a variable and an environment variable in `bash`. The normal convention is to name local variables in all lowercase or in mixed\-case characters. An environment variable, however, is usually always in all uppercase letters.

# Checking out commonly used environment variables

The bash shell has many environment variables. You may be amazed at the range of items these variables store. The handy thing is that, if something is stored in a variable, you can change it to suit your needs! In Table 16\-1, I list the environment variables you’re most likely to want to work with.