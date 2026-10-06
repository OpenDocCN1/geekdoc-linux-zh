The Shell's Responsibilities 49

![](bbox=[0.14, 0.111, 0.513, 0.163])

Figure 2.13 Execution of wc -l < users

When we begin execution this time, it sees that it passed the single argument -1. Because no filename was specified, we decides that the number of lines coming in standard input should be counted instead. So wc -1 counts the number of lines, unaware that it's actually counting the number of lines in the file users. The final tally is displayed as usual, but without the name of a file we wasn't given one.

The difference in execution of the two commands is important for you to understand. If you're still unclear on this point, review the preceding section one more time before proceeding.

# Hooking up a Pipeline

Just as the shell command line for redirection characters, it also looks for the pipe character ; For each command, it connects the standard output from the preceding command to the standard input of the latter, then initiates execution of both programs.

So when you type who | -1

the shell finds the pipe symbol separating the commands who and wc. It connects the standard output of the former command to the standard input of the latter, then initiates execution of both. When the who command executes, it produces a list of who's logged in and writes the results to standard output, unaware that this is not going to the terminal but another command.

When we command executes, it recognizes that no filename was specified and counts the lines on standard input, unaware that standard input is not coming from the terminal but from the output of the who command.

As we proceed, you'll see that not only can you have two-command pipelines; you can string together three, four, five, or more commands in really complicated pipelines too. It's a bit tricky to figure out, but thats really where the greatest power of the Unix systems lies.

# Environment Control

The shell provides certain commands that you can customize your environment. Your environment includes your home directory, the characters that the shell displays to prompt you to type in a command, and a list of the directories to be searched whenever you request a program be executed. You'll learn more about this in Chapter 10.