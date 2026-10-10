| Command | Action |
| :------- | :------ |
| date | Displays the current date and time. The root user can also use this command to change the date and time. (See man page for more info.) |
| man command | Displays the manual page for *command*. (See Chapter 7.) |
| vi | Invokes the vi text editor. If a filename is specified, that file will be opened. (See Chapter 6, “Working with Applications.”) |
| ee | Invokes the FreeBSD Easy Editor. If a filename is specified, that file will be opened. (See Chapter 6.) |

# System Utilities and Maintenance-Related Commands

| Command | Action |
| :------- | :------ |
| ps | Displays the list of processes running on the system. Common options include -1 for a detailed list, -a for all processes, and -x to display daemon processes as well. (See Chapter 13, “Performance Monitoring, Process Control, and Job Automation.”) |
| top | Displays a list of processes and their resource usage statistics that is updated on a regular basis. (See Chapter 13.) |
| kill n | In this command, *n* is the process ID number you wish to kill. Options are available to send different signals to the process. (See Chapter 13.) |
| killall pname | In this command, *pname* is the name of the process to kill. All processes that match and belong to you will be killed. Options are available to send different signals to each process. (See Chapter 13.) |
| at | Schedules a job or command to run at a specified time. (See Chapter 13.) |
| crontab filename | Schedules jobs or commands to run on a regular basis. *filename* is the name of the crontab file you want to edit. (See Chapter 13.) |
| shutdown | Shuts down or reboots the system. (See Chapter 4, “Your First Session with FreeBSD.”) |
| halt | Halts the system. (See Chapter 4.) |
| reboot | Reboots the system. (See Chapter 4.) |

# Printer-Related Commands

| Command | Action |
| :------- | :------ |
| lpr | Sends a job to the printer. (See Chapter 15, “Printing.”) |
| lprm n | In this command, *n* is a job number. This removes the job from the printer. Other options allow removing jobs for a particular user, and so on. (See Chapter 15.) |
| lpq | Displays the list of jobs currently in the printer queue. (See Chapter 15.) |
| lpc | Controls the printer queues and the print daemons. (See Chapter 15.) |