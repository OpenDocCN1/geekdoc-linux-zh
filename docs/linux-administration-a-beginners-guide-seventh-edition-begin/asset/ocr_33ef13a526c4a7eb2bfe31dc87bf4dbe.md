# 50 Linux Administration: A Beginner's Guide

commands. At any given time, you can find out how many jobs Bash is tracking by typing this command:

```
$master@server -$ jobs
[1]+ Running firefox &
```

The running programs that will be listed be in one of two states: running or stopped. The preceding sample output shows that the Firefox program is in a running state. The output also shows the number in the first column—[1].

To bring a job back to the foreground—that is, if you give back control of the terminal—you would use the fg (foreground) command, like this:

```
$master@server -$ fg NUMBER
$master@server -$ fg 1
firefox
```

Here, NUMBER is the job you want in the foreground. For example, to place the Firefox program (with job number 1) launched earlier in the foreground, type this:

If a job stops (in a stopped state), you can start it running again in the background, allowing you to keep control of the terminal and resume the job. A stopped job can run in the foreground, which gives control of the terminal back to program.

To place a running job in the background, type this

```
$master@server -$ bg NUMBER
```

Here, NUMBER is the job number you want to background.

> NOTE You can background any process. Applications that require terminal input or output will be put into a stopped state if you background them. You can, for example, running the top utility in the background by typing top &. Then check the state of that job with the jobs command.

# Environment Variables

Every instance of a shell, every process that is running, has its own 'environment'— these are settings that give it a particular look, feel, and in some cases, behavior: These are typically controlled by environment variables. Some environment variables have special meanings to the shell, but there is nothing stopping you from defining your own and using them for your needs. It is through the use of environment variables that most shell scripts are able to do interesting things and remember results from user inputs as well as program outputs. If you are already familiar with the concept of environment variables in Windows 200x/XP/Vista/7/8/10, you'll find that many of the things you know will apply to Linux as well; the only difference is how they are set, viewed, and removed.