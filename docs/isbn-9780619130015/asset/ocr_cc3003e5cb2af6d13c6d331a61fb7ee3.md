**2**  Continue to run the top utility in the background. The process is the subject of the next two exercises.

The ps command shows you a list of the processes currently running. When you use the command with no options, it shows a list of the processes associated with the current login session. When used with the –A option, it shows a very long list of all processes running on the system.

# To use the ps command:

**1**  Type **ps** and press **Enter**. Your screen looks similar to Figure 8-18.

![](bbox=[0.21, 0.35, 0.79, 0.72])

**2**  The output of the ps utility includes this information about each process:

+   - PID
- Name of the terminal where the process started
- Amount of time the process has been running
- Name of the process

Notice the top utility still runs in the background.

**3**  To see a list of all processes running on the system, type **ps –A | more** and press **Enter**. Figure 8-19 shows an example of the command’s output.