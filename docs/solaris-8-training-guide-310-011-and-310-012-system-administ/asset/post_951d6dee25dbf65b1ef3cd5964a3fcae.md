
## APPLY YOUR KNOWLEDGE

3. Enter the following after the last line at the end of the file:

```
0 11 * * * echo Hand in Timesheet > \
/dev/console
```

4. Save and close the file.

Open a console window and at 11:00 a.m., you'll see the message “Hand in Timesheet” displayed.

## Review Questions

1. Which of the following commands finds all processes that have “dt” in the process argument string? Choose all that apply.

+   A. pgrep -l -f "dt"
B. ps -ef "dt"
C. ps -el "dt"
D. ps -ef|grep dt

2. Which commands can be used to monitor system processes:

+   A. prstat
B. psrset
C. ptree
D. sdtprocess

3. Which one of the following commands kills a process named test?

+   A. pkill -9 test
B. kill -9 test
C. ps -ef|grep kill| kill -9
D. kill test

4. Which commands display active system processes and update at a specified interval? Choose all that apply.

+   A. ps
B. prstat
C. sdtprocess
D. ptree

5. In output from the ps command, what does an “R” stand for in the S field:

+   A. The process is on the run queue.
B. The process is receiving input.
C. It is a regular process.
D. The process is sleeping, so it must be restarted.

6. In output from the ps command, which of the following does the UID field display?

+   A. The parent process
B. The process id
C. The process owner
D. The priority of the process

7. Which one of the following options to the ps command lists only processes for a particular user?

+   A. -P
B. -f
C. -l
D. -u

8. Which one of the following options to the ps command lists only processes associated with the local terminal?
A. -l
B. -a
C. -f
D. -t

9. Which one of the following sends a terminate signal (signal 15) to a process with a PID of 2930?
A. kill 2930
B. stop 2930
C. Ctrl+C
D. cancel 2930

10. Which one of the following signals stops a process unconditionally?
A. 9
B. 0
C. 15
D. 1

11. Which one of the following commands is used to change the priority on a process?
A. nice
B. priocntl
C. ps
D. hup

12. Which one of the following commands is issued to increase the priority of PID 8200?
A. renice -n -4 -p 8200
B. nice -n -4 -p 8200
C. nice -i 8200
D. renice -I -p 8200

13. Which utilities can be used to show the process ancestry tree? Choose all that apply.
A. ps
B. ptree
C. sdtprocess
D. prstat

15. Which two of the following commands schedules a command to run once at a given time?
A. crontab
B. priocntl
C. at
D. cron

16. Which one of the following commands shows the jobs queued up by the at command?
A. atq
B. at -l
C. ps
D. crontab

17. Which one of the following crontab entries instructs the system to run logchecker at 3:10 on Sunday and Thursday nights?
A. 0 4 * * 10,3 /etc/cron.d/logchecker
B. 10 3 * * 0,4 /etc/cron.d/logchecker
C. * 10 3 0,4 /etc/cron.d/logchecker
D. 10 3 * * 0-4 /etc/cron.d/logchecker

18. Which one of the following is the daemon responsible for capturing system messages?
A. syslogd
B. messaged
C. init
D. msgd

19. Which one of the following is the line in the /etc/syslog.conf file that sends all alert messages to user root?
A. *.alert  root
B. alert root
C. root *.alert
D. *.emerg root

20. Which one of the following logs keeps a record of all cron activity?
A. /var/cron/log
B. /var/spool/cron/log
C. /var/adm/cron
D. /var/adm/messages

21. At which run level is the syslog daemon started?
A. 2
B. 1
C. 3
D. It runs at all run levels.

22. Which one of the following files holds the most recent login time for each user in the system?
A. /var/adm/lastlog
B. /var/adm/messages
C. /var/adm/acct
D. /var/adm/utmpx

23. A user wants to execute a command later today, after leaving work. Which one of the following commands will allow him to do this?
A. runat
B. at
C. submit
D. None of the above

## Answers to Review Questions

1. A., D. Use the pgrep and ps commands to view processes running on your system. The commands pgrep -l -f "dt" and ps -ef | grep dt find all the processes that have “dt” in the process argument string and display them.

2. D. New in Solaris 8 is CDE Process Manager, sdtprocess, a graphical Common Desktop Environment (CDE) tool that provides a process manager window for monitoring and controlling system processes.

3. A. The command pkill -9 test kills a process named test.

4. B., C. The prstat and sdtprocess commands display active system processes, and can be configured to update at a specified interval.

5. A. In output from the ps command, the “R” in the “S” field means that the process is on the run queue.

6. C. In output from the ps command, the UID field displays the process owner.

7. D. The -u option to the ps command lists only processes for a particular user.

8. B. The -a option to the ps command lists only processes associated with the local terminal.

9. A. The command kill 2930 sends a terminate signal (signal 15) to a process with a PID of 2930.

10. A. Signal 9 stops a process unconditionally.

11. A., B. The commands nice and priocntl are used to change the priority on a process.

12. A. The renice -n -4 -p 8200 command is issued to increase the priority of a process with a PID of 8200.

13. B., C. The utilities ptree and sdtprocess are used to show the process ancestry tree.

14. C. The at command schedules a command to run once at a given time.

15. A., B. The atq and at -l commands show the jobs queued up by the at command.

16. B. The crontab entry 10 3 * * 0,4 /etc/cron.d/logchecker instructs the system to run logchecker at 3:10 on Sunday and Thursday nights.

17. A. The syslogd is the daemon responsible for capturing system messages.

18. A. The entry *.alert root in the /etc/syslog.conf file, tells syslogd to send all alert messages to user root.

19. A. The log file named /var/cron/log keeps a record of all cron activity.

20. A. The syslog daemon is started at run level 2.

21. A. The file /var/adm/lastlog holds the most recent login time for each user in the system.

22. B. Use the at command to execute a command or script at a later time.

## OBJECTIVES

The following are the test objectives for this chapter.

## Understand the Solaris LP print service

- Setting up and administering printers in Solaris requires an understanding of the print spooler, the print daemons, and the printer configuration files. Each of these will be described in this chapter.

## Manage printers

- Managing printers in Solaris 8 involves using several utilities and commands. These commonly used utilities and commands will be described in this chapter.

## CHAPTER 10

## LP Print Service

## OUTLINE

Introduction 378

Administering Printers 393

The Solaris Print Service 378

Deleting Printers and Managing Printer Access 393

LP Print Service Directories 379

Creating Printer Classes 395

The Print Spooler 380

Checking Printer Status 397

The LP Print Daemons 381

Managing Printer Queues 398

Setting Up the Hardware 382

Restarting the Print Scheduler 405

Ethernet Connection 383

Setting a User's Default Printer 406

Parallel Connection 383

Modifying the Printer with Admintool 407

Serial Connection 383

Summary 408

Setting Up the Software 384

Apply Your Knowledge 409

BSD versus SVR4 Printing Software 384

Print Server versus Print Client 387

Configuring Software for a Solaris Printer 388

Using a Printer Not Listed on the Printer Types Menu 392

## STUDY STRATEGIES

The following strategies will help you prepare for the test:

- In this chapter, you’ll notice that I don’t show many lengthy step-by-step procedures, but I do introduce several commands used to manage printers, along with examples on how to use the commands. Practice the step-by-steps as well as the commands, and make sure that you understand where and when to use them.
- Pay close attention to the differences between the SVR4 and the BSD style print services.
- Make sure that you understand the difference between a print server and a print client. Understand the differences between local and networked printers, and pay close attention to the various configuration files that are used to define a printer.
