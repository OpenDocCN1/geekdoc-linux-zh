# Lesson 14

many error messages, or quite simply, your script will not work properly. This is very important since the syntax of different shells will almost always vary.

Now, after you set up the script with the correct indicator of what shell to use, enter some commands.

```
#!/bin/bash
echo "Hi this is Unix speaking, I know who you are, you are $USER"
echo "Your current directory is also known, it happens to be, $PWD"
ls # note script used to check user, directory and list files
```

What do we have here? Well, without panicking (this is common to when you see something like this) pick it apart, by piece.

The first line sets the field. The second line uses the $USER variable to echo back your username (in this case I happen to be logged in as root). The third line is identical to the second except you see the $PWD variable in use; this tells you your current directory location. The fourth line tells Unix to list the contents of the current directory. Each of these commands one at a time will simulate the script executing one line at a time. This can also be placed in one file (master emacs or vi) and executed as a script file by a user or another program like at or cron.

Remember, this script should be populated with commands that bash can handle and process; therefore, this is why you may not have noticed some of these commands or they may not be available on your version of Unix. This is why it is important to master the basics so you can do scripting in the first place. As you can see from our example, some comfort with your shell is needed.

Keep going over this example until you understand it completely. It is important to learn how to do scripts if you are going to be a Unix administrator. For end users, you may never need to create a script, but you may consider that your current employer expects you to come in every day and run a certain amount of jobs. Remember the jobs command? That could