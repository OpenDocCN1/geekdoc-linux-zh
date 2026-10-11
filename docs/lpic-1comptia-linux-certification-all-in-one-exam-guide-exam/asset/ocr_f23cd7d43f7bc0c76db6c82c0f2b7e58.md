+   C. stayalive
+   D. kill -NOHUP

+   16. It's currently 1:00 in the afternoon. You want to schedule the myapp program to run automatically tomorrow afternoon at 12:00. Which of the following at commands could you use? (Choose two.)
+   A. at 12 pm tomorrow
+   B. at tomorrow -1 hour
+   C. at now +1 day
+   D. at today +23 hours
+   E. at now +23 hours

+   17. Which of the following crontab lines will cause the /usr/bin/myappcleanup process to run at 4:15 a.m. on the first of every month?
+   A. 15  1  *  *  *  /usr/bin/myappcleanup
+   B. 15  4  *  1  *  /usr/bin/myappcleanup
+   C. 1  4  15  *  *  /usr/bin/myappcleanup
+   D. 4  1  *-*  *  15  /usr/bin/myappcleanup

# Answers

+   1. D. A multitasking operating system constantly switches CPU time between loaded processes, creating the impression that the CPU is actually executing processes concurrently.
+   2. A. Because the command was entered from the shell prompt, a user process was created.
+   3. A. Because the command was entered from the shell prompt, its parent process is the bash process, which has a PID of 3456.
+   4. B. The init process is the grandparent of all other Linux processes on the system. All other processes can trace their heredity to init.
+   5. B. The init scripts for distributions that use System V init scripts are stored in /etc/rc.d/init.d.
+   6. C. The ps -f command will display extended information about processes associated with the current shell session.
+   7. A. A zombied process is one where the process has finished executing, but the parent process wasn't notified and, therefore, hasn't released the child process's PID.
+   8. B. The ps -e command can be used to display a list of all running processes on the system.