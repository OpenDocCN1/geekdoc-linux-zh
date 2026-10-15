# Extra

You can control various properties that specify how the scheduler, the management the operating system provides to switch between threads on a system, chooses to run a thread. The IsBackground property enables or disables background running. If a thread inside your application is a background thread, the thread automatically exits when your program exits. If the thread is a foreground thread, IsBackground = False, the program does not exit until the thread completes, just like the main application thread. You can control the priority of a thread in Visual Basic .NET using the Priority property. The priority determines how often a thread runs when the system multitasks. You can set the Priority property to one of the constants from the ThreadPriority enumeration. The values, from highest to lowest in terms of run-time, include: Highest, AboveNormal, Normal, BelowNormal, Lowest. You can set threads that run in the background, for example an automatic save, to below normal priorities. The default priority is Normal. Using priorities above normal gives the thread a majority of processor time at the expense of the user’s ability to use the system seamlessly.

![](bbox=[0.065, 0.5, 0.5, 0.82])

![](bbox=[0.52, 0.5, 0.945, 0.82])

# STOP EXECUTION

6 To stop execution, type newThread.Abort(), replacing newThread with the object variable.

7 Type the object variable again and follow it with .Join().

8 Press F5 to run your project.

The thread responds to commands.