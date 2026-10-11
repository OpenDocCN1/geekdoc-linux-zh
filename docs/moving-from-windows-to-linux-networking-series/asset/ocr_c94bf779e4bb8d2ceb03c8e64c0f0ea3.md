viruses.

The `env` command provides you with all the current environmental variables. Environmental variables will be specific to a given user. This means that if you run the `env` command while a different user is logged in, you may get different results. Environmental variables cover many aspects of the user's environment. The home directory, current user, and current history size are all environmental variables.

The `path` statement is also a very important environmental variable. The `path` statement lists all the paths in which the operating system will look for a command when you type it in the shell. All the commands we study are actually programs somewhere on your machine. The `path` statement tells the shell where to look for commands you enter. This is important because there are some software packages you may install, particularly programming tools such as Java, that ask you to add one of their directories to the `path`. The `env` command's display is shown in Figure 18.10.

![](bbox=[0.06, 0.23, 0.67, 0.54])

The `kill` command is perhaps the simplest command of all. You enter the word `kill` followed by the process ID (PID). An example is `kill 1045`. Be very careful with this command. If you `kill` a process the system requires, you could cause the system to function improperly or even crash. This is one reason why you don't want people to log in as root. Only root can `kill` a system process. If a user is logged in under a user account, he cannot `kill` a system process.