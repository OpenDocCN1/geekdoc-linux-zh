Of course, no one wants to keep typing --preserve-root each time they run rm, so you should add this line to the .bashrc file in your home directory:

```
alias rm='rm --preserve-root'
```

That alias automatically adds --preserve-root to all calls to rm in future Bash sessions.

# Printing the Last Lines of a File with tail

If you want to watch a log file as it is written to, or want to monitor a user's actions as they are occurring, you need to be able to track log files as they change. In these situations you need the tail command, which prints the last few lines of a file and updates as new lines are added. This command tells tail to print the last few lines of /var/log/httpd/access_log, the Apache hit log:

```
tail /var/log/httpd/access_log
```

To get tail to remain running and update as the file changes, add the -f parameter (follow):

```
tail -f /var/log/httpd/access_log
```

You can tie the lifespan of a tail follow to the existence of a process by specifying the -p id parameter. When you do this, tail continues to follow the file you asked for until it sees that the process identified by PID is no longer running, at which point it stops tailing.

If you specify multiple files on the command line, tail follows both, printing file headers whenever the input source changes. Press Ctrl+C to terminate tail when in follow mode.

# Printing Resource Usage with top

The top command is unusual in this list because the few parameters it takes are rarely, if ever, used. Instead, it has a number of commands you can use while it is running to customize the information it shows you. To get the most from these instructions, open two terminal windows. In the first, run the program yes and leave it running; in the second run sudo top.

The default sort order in top shows the most CPU-intensive tasks first. The first command there should be the yes process you just launched from the other terminal, but there should be many others also. First, we want to filter out all the other uses and focus on the user running yes. To do this, press u and enter the username you used when you ran yes. When you press Enter, top filters out processes not being run by that user.

The next step is to kill the process ID of the yes command, so you need to understand what each of the important fields means:

+   PID—The process ID
+   User—The owner of the process