
## MORE ADMINISTRATIVE TASKS

**FIGURE 11-3**
User cron mail result.

![](img/37f079cee226b270f2e09b37a2e4a05d_304_0.png)

### NOTE

The sendmail service is an e-mail transport agent. It sends a message to one or more recipients, routing the message as necessary. This program is the service that must be running to use local mail accounts. To start sendmail, use the following command:

`service sendmail start`

The **mail** command is used to send and receive mail. It has a very simple command-line interactive interface. To read mail use the **mail** command.

You are presented with a list of e-mail message headers. The headers list who the e-mail is from, date/time, and subject. The following commands will give you a list of your e-mail. Use the `man mail` command for a complete list of options.

- **enter** to go through the list of e-mail.
- **delete** to delete the current message. You can delete a list of messages by using a range, such as **delete 1-5**.
- **quit** to end the mail session.

To send an e-mail, use the **mail mail_recipient** command where mail_recipient is the To: entry in the e-mail. Figure 11-4 displays the sequence to send a message to root.

The user jsmith enters **mail root** to indicate that the e-mail is to be sent to root. The system responds with the prompt **Subject**: asking jsmith to enter a subject line for the e-mail. jsmith enters a subject and presses Enter. He then enters the body of the message and at the end uses Ctrl+d to indicate the end of the message. The system then asks if there is a Cc: recipient for the message. When jsmith enters this, the mail is sent.

The root user enters **mail** to receive the e-mail for the root account. One header is displayed with the number 1 next to it. To display message 1, root enters a **1** and presses Enter. The message is displayed. To exit the mail program, the user root types the **quit** command and presses Enter.

User cron jobs are copied by the crontab command into the /var/spool/cron directory. The filename is the username. This file should not be edited; rather edit the user's crontab file and rerun the crontab command.

![](img/37f079cee226b270f2e09b37a2e4a05d_305_0.png)

One of the simplest ways to manage your crontab file is to use the **crontab -e** command. This command will open the user's crontab file in the editor specified in the user's EDITOR environment variable. The command crontab -l will list the user's crontab file. In addition the cron daemon will log its activities in the file /var/log/cron, which can be very useful to a system administrator when troubleshooting cron problems.

## MANAGING CORE DUMPS

In the early days of computers, the type of memory used was magnetic core memory (Figure 11-5). Core memory was a group of metal donut shapes with wires running through the center of the cores. When electrical current was applied through the wires, the core they intersected would change magnetic polarity. This caused the core to have a magnetic field that the computer would interpret as either a 1 or a 0. A third wire was used to sense the value of the core position. When there was a problem, the core contents would be printed and then deciphered. This output was called a **core dump**. The term stuck and is still used today, even though the only place you can find a core is on antique machines.

![](img/37f079cee226b270f2e09b37a2e4a05d_305_1.png)

Many Linux systems automatically create a core dump when a program fails. The Linux operating system usually puts a file named *core* in the directory the program was run from.

### Understanding a Core Dump

A core dump is a recording of what was in memory at the time of program failure. The reasoning here is that a programmer can take the core dump and determine what went wrong during program execution. But with the number and types of tools available today, the chance of a programmer using a core dump file is very small.

When a program crash causes a core dump, the file that is written to disk varies in size. The contents of the file will be everything that pertains to the file that was in memory at that particular time. Larger files will have larger core dumps.

### Managing Core Files

Core files can be restricted in size or even eliminated with the **ulimit** command. The ulimit command will, among other things, limit the *size* of core dumps. To limit the size of a core dump to 100K, use the command *ulimit -c 100*.

The *-c* option sets the maximum core dump value. In many systems, you should use a value of 0 to prevent any core dumps. The default value for core dumps on Red Hat Linux is 0. Use a value of *unlimited* if you want the maximum core dump saved to disk.

To find any core dump files on the system, use the **find** command. To find all core dumps starting in the root (/) directory, use the command *find / -name core*. **find** is the command, */* is the starting directory, the *-name* option says to use a pattern, and *core* is the pattern to look for. You can get the owner and creation date of the core file from a directory listing of the file. To see which program caused the dump, try using the **gdb**, GNU Debugger, program. *gdb* performs a lot of different functions, but the *-c* option will examine a core dump and return the program name that generated it as well as other information. To see the information about a core dump, use the *gdb -c core* command.

The directory listing can also be produced with the *find* command. For example, *find / -name core -type f -ls* will find all core files and produce a directory listing. The *-type f* command will suppress listing directories named *core*.

You can easily delete unneeded core files. You could even write a cron job that searches for core files and then deletes them. But keep in mind that a core dump indicates a problem with a program. If you are getting several core dumps, you need to have someone available to check the files.

## MANAGING PROCESSES

A process is a program that is currently running on Linux. Any program running on the system is termed a process. The shell in which you type in commands is a process. The **ls** command is a process. The Web browser is a process. Each of these programs can run other processes, and at any given time hundreds of processes can be running.

Because the Linux operating system is a multiserver, multitasking operating system, each user on the system can run multiple processes. If user *jnjsmith* is connected and using *vi*, and *root* is also connected and running *vi*, *vi* will be associated with two processes. Even a single user can have multiple copies of a program running at the same time. Tracking processes becomes extremely important when you have multiple users running processes.

Managing processes is one of the major duties of a Linux administrator. An admin has the power to kill a process, restart a process, or give it a different priority. When a process is started, it is assigned a process ID (PID). The PID is used to manage and monitor the process.

### Using ps

One of the tools used to manage processes is *ps*. The *ps* command gives a list of the processes that are currently running at the moment in time it is executed. *ps* has many options and, on most Linux systems, can accept options of different types. The reason there are different types of options is that *ps* has been used on a lot of different Unix/Linux versions. Not all implementations are the same, so multiple option types have been included to enable all users to use the software without learning new syntax. The types of options available are the following:

- **UNIX98** Options may be grouped and must follow a hyphen (-). For example, the *ps* command with grouped options *e* and *f* would be *ps -ef*.
- **BSD** Options may be grouped and must not follow a hyphen. The same *ps* command would be *ps ef*.
- **GNU** Options may not be grouped and the *long* options follow two hyphens. To use the *ps* command to list processes for a specific user, use the *--user* command: *ps --user jsmith*.

![](img/37f079cee226b270f2e09b37a2e4a05d_307_0.png)

> The default behavior of the *ps* command can be modified by setting the environment variables *PS_PERSONALITY* or *CMD_ENV* to one of the following values: *posix*, *old*, *linux*, *bsd*, *sun*, or *digital*.

Table 11–2 shows the fields that describe the processes that are running.

**Table 11–2**
Field descriptions.

| Field | Purpose |
| --- | --- |
| %CPU | Indicates the percentage of CPU time the process is using. This number varies greatly, depending on the process and what it is doing. |
| %MEM | The percentage of memory the program is using. This value will change, depending on what the process is doing. |
| CMD or COMMAND | What command is running. The name of the process. |
| PID | Process ID. This unique number is assigned when the process is started. This value is used to refer to a process. |
| PPID | Identifies the Parents Process ID. |
| PRI | The priority level of a process. The default value is 0. A value of 20 will run only when nothing else in the system wants to run. Any negative value causes the process to run faster. A user may control only his own processes. |
| RSS | The Resident Set Size is the kilobytes of the program in memory. |
| SIZE | Total memory size of the process's code, data, and stack. |
| STAT | Displays the state of the process. R for running, S for sleeping, D for uninterruptible sleep, t for stopped, and Z for zombie. |
| TIME | The total CPU time used since the process was started. |
| TTY | The terminal identification. Not all processes are associated with a TTY, as some are started by other processes. X programs do not have TTY numbers. |
| USER | The name of the user that executed the process. |

The *ps* syntax is *ps [options]*. The following are some of the more useful *ps* options. Use *man ps* for a complete list of options.
