plan to use, your backup schedule, the software you intend to use, commands or procedures to perform backups (perhaps including scripts to be called by cron), and a plan for restoring data (both partial and full restores). If possible, you should implement and test your backup plan. If this isn't possible and you're administering a true production Linux system, make it possible. Murphy's Law applies to backups, and if you don't plan for disaster, it will strike.

# Task 3.5: Manage Running Processes

Running processes must sometimes be monitored and even terminated. You might want to monitor a process if you have reason to believe it might consume undue amounts of CPU time or if the process is taking a long time to do its job. If you conclude that the process is hung (that is, unresponsive to input), is working but is consuming too much CPU time, or is otherwise misbehaving, you may want to terminate it.

# Scenario

Users of a multi-user Linux system are reporting sluggish performance. You must troubleshoot this problem and, if appropriate, terminate any program that's misbehaving or simply consuming too much CPU time.

# Scope of Task

This task involves checking running processes in various ways and terminating those processes. Most of the commands are fairly simple, but some of them have many options.

# Duration

This task should take about half an hour to complete, although you can spend more time studying all the ps options if you like. Performing simple checks of processes can take just a few seconds, but you may want to do this job multiple times each day on a working system. In fact, for critical systems, you might want to set up a cron job (described in Task 3.8) to perform checks of system load on a regular basis.

# Setup

You need access to a working Linux system with an X server installed. You should log into your Linux system as an ordinary user; root access is not required to complete this task, although in real situations it often is needed. In order to simulate an out-of-control process, you should launch glxgears from X. The glxgears program is a simple program to test the speed of OpenGL 3D extensions to X; it produces a window in which three simulated 3D gears spin continuously. Every few seconds, it displays benchmark data in frames per second (FPS). The point of using glxgears is that it tends to hog CPU time, similar to the way many out-of-control programs do, enabling you to practice tracking excessive CPU use.