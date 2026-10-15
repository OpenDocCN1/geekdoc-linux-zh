One way to submit jobs to at is via stdin. Alternatively, you can feed a file containing the commands to be executed into at, as shown in Listing 2.26.

# LISTING 2.26 Execution of at Using a File

```
Rank Execution Date Owner Job Queue Job Name
3rd Jun 23, 2004 14:00 root 1087992000.a a stdin
root@unixhost:>

root@unixhost:> cat my_cmds1.txt
cd ./HO/myt est1
ls -l /tmp > tmplist.lst

root@unixhost:> at -f my_cmds1.txt now + 2 minutes
commands will be executed using /sbin/sh
job 1087395867.a at Wed Jun 16 16:24:27 2004
root@unixhost:> atq
Rank Execution Date Owner Job Queue Job Name
1st Jun 16, 2004 16:24 root 1087395867.a a my_cmds1.txt
2nd Jun 18, 2004 14:00 root 1087560000.a a stdin
3rd Jun 18, 2004 17:11 root 1087571471.a a stdin
4th Jun 23, 2004 14:00 root 1087992000.a a stdin
5th Aug 15, 2004 17:07 root 1092584233.a a stdin
root@unixhost:>
```

The advantage of using a file containing the commands to be executed is obvious; instead of stdin, the name of the command file is displayed as job name. Jobs supposed to run in a distant or even a not-so-distant future should be submitted via a command file, thus saving the guesswork of what the job in question will do. By using a very descriptive name, you reveal the purpose of the chain of commands to be executed.

However, if the jobs either are scheduled via the command line or are given a command file name that is not descriptive enough, it is possible to check the contents of all at jobs. Depending on the flavor of *NIX, all information will be stored in a directory, for example, in /var/spool/cron/atjobs on Solaris. Listing 2.27 shows the Solaris job ticket.

# LISTING 2.27 Contents of a Job Ticket (Solaris)

```
# pwd
/var/spool/cron/atjobs
# cat 1087560000.a
: at job
```