# Using at

The at command gives you the ability to run a program once, at a specified time. A variant program, batch, lets you tell the system to run a program when the system load drops low enough (specifically, below 1.5). The syntax for these commands is

```
at [-V] [-q queue] [-f file] [-mldbv] time
batch [-V] [-q queue] [-f file] [-mv] [time]
```

The options to these commands are

+   -V
+       Displays the version number of the program.

+   -q queue
+       The at command supports multiple queues, each of which is identified with a letter (a to z and A to Z). Normally, at uses queues with lowercase letters, and batch uses queues with uppercase letters. The default queues for at and batch are c and E, respectively. Queues with later letters run with lower priority.

+   -f file
+       Normally, you type the command you want to run after you type the at or batch command, then press CTRL-D, which is a standard FreeBSD end-of-file indicator. Alternatively, you can enter the command in a file and pass the filename to at or batch. This method is especially useful if you want to run a script as the command; you can simply pass at the name of the script.

+   -m
+       This option sends mail to the user who runs the job when the job finishes.

+   -l
+       Causes at to display jobs that are currently queued. This option is equivalent to typing atq.

+   -d
+       Deletes a job from the queue. The at rm command does the same thing.

+   -b
+       Causes at to work like batch.

+   -v
+       When used with -l, displays jobs that are completed but haven't yet been removed from the queue.

+   time
+       The time for the job to run. You can use several formats for this specification, including HH:MM or HH:MM to run a job at a given time in the next 24 hours, with an optional AM or PM suffix. The strings noon, midnight, and teatime (4:00 PM.) also work. To specify a run time more than 24 hours in the future, you can provide a date after the time specification. The date can take the form MMDDYY, MM. DD. YY, MM/ DD/ YY, or month-name day year. You can also give the time in a relative form by giving a plus sign (+), a value, and units, such as +30 minutes.

In a default FreeBSD installation, only root may run at or its related commands. You can change this restriction by adding the files /var/at/at.allow or /var/at/at.deny. To give only a few specific users permission to use these commands, create