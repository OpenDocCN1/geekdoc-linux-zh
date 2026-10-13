which is located in the parent directory of the current directory—you could use the command `cd ../my_stuff.`

![](bbox=[0.22, 0.27, 0.27, 0.38])

> If you get lost in the FreeBSD directory structure, you can instantly return to your home directory by typing `cd` followed by pressing the Enter key. The `cd` command with no arguments will always take you back to your home directory no matter where you currently are in the directory tree.

# The pwd Command

If you can't remember what directory you are currently in, the `pwd` command will list it for you. `pwd` stands for *print working directory*. There is a way to make the current working directory a part of your shell prompt so that the prompt always shows you what directory you are currently in. We will look at how to do this in Hour 5, “Advanced UNIX Shell Use.”

# Creating Files

There are several ways to create an empty file in FreeBSD. For our purposes right now, we are going to use the `touch` command. If you are not already in it, change to the directory we created earlier called `mydir` using the `cd` command discussed previously. Now enter the command `touch myfile`. This will simply create an empty file called `myfile` in the current directory. Of course, empty files are not very useful, but this will allow you to look at some basic file manipulation commands.

![](bbox=[0.22, 0.78, 0.27, 0.89])

> The tilde character, `~`, is shorthand for your home directory. It can be used anywhere that you want to refer to your home directory. For example, `cd ~/documents` will take you to the `documents` directory located within your home directory no matter where you currently are in the directory tree.

# Moving Files

The command to move a file from one place to another is `mv`. Try the following command:

`mv myfile myfile1`

This command will simply move `myfile` to a new file called `myfile1`. Of course, you can also think of this as simply renaming the file. However, the behavior of `mv` will