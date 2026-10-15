# 10.6 PROCESS AND JOB CONTROL

UNIX is responsible for several activities related to process and job management, including process creation, process termination, running processes in the foreground and background, suspending and resuming processes, and switching processes from foreground to background and vice versa. As a UNIX user, you can request the process and job control tasks by using the shell commands discussed in this section.

# 10.6.1 Foreground and Background Processes and Related Commands

When you type a command and hit <Enter>, the shell executes the command and returns by displaying the shell prompt. While your command executes, you do not have access to your shell and therefore cannot execute any commands (i.e., continue work) until the current command finishes and the shell returns. When commands execute in this manner, we say that they execute in the foreground. By default, every process runs in the foreground, taking input from the keyboard and sending output to the display screen.

UNIX allows you to run a command so that, while the command executes, you get the shell prompt back and can submit other commands. This capability is called running the command in the background. You can run a command in the background by ending the command with an ampersand (&). Of course, in a graphical environment, you can run a command in one terminal window in the foreground, open another terminal window, and use the shell in the new terminal window. However, this activity takes time and consumes additional system resources.

Background processes run at lower priorities compared to their foreground counterparts. Thus, they get to use the CPU only when no higher priority process needs it. When a background process generates output that is sent to the display screen, the screen looks garbled, but if you are simultaneously using another application, your work is not altered in any way. You can get out of the application and then get back into it to obtain a cleaner screen. Some applications such as vim allow you to redraw the screen without quitting it. In vim (see Chapter 3), pressing <Ctrl+L> in Command mode allows you to do so.

The syntaxes for executing commands in the foreground and background are as follows. Note that no space is needed between the command and & but that you can use space for clarity.

```
SYNTAX
command (for foreground execution)
command & (for background execution)
```

Now consider the following command executed under the Bourne shell. It searches the whole file structure for a file called foo and stores the pathnames of the directories that contain this file in the file foo.paths. The error messages are sent to the file /dev/null, which is the UNIX black hole: whatever goes in never comes out. Note that, for the C shell,