
## The Printing Daemon

Linux distributions use varying methods to support printers but, by far, the most common is the Berkeley Software Distribution (BSD)-derived print spooling daemon called /lpd. Started by a script that runs automatically every time your system is booted, /lpd begins by scanning a file called /etc/printcap. This file contains printer definitions, which must be entered in accordance with strict rules of syntax. Subsequently, /lpd waits for requests for print services. When such requests are made, /lpd writes the file temporarily to /var/spool and begins feeding the data to the printer. If /lpd receives additional printing requests before the first job is finished, the daemon creates a print queue, a list of files waiting to be printed.

## The Printer Configuration File

Printer definitions are stored in /etc/printcap. Although you can edit this file manually, you should not do so if it was created by a printer configuration utility. Should you need to make changes to your printer configuration, run the utility again. Linuxconf, a system administration utility discussed in this chapter, includes a printer configuration utility. You should edit this file directly only if you want to take advantage of a special printer feature that your printer configuration utility does not support.

Entries in /etc/printcap must conform to the following rules:

- Each printer definition must be entered on one line only. To make the file more readable, you can break a line with a backslash (\). Make sure you don't enter a space or Tab character after the backslash.
- The first field contains the printer's name.
- Additional fields are separated by colons and begin with a printcap variable (see the table Printcap Variables in this section).
- Some variables are Boolean and are assigned if they are present in the file. Others are assignment variables and require an equals sign, for example, sd=/var/spool/lpd/lp. Still others are numeric variables and require the numeric operator (#), as in this example: mx#0.
- The printer named lp is the default printer.

The following is an example of a valid entry for the default printer *lp*. A network-accessible LaserJet printer is described.

```
lp: \
:sd=/var/spool/lpd/lp: \
:mx#0: \
:sh: \
:rm=192.168.100.3: \
:rp=raw: \
:if=/var/spool/lpd/lp/filter:
```

### PRINTCAP VARIABLES

| Use This Variable | To Do This |
| :--- | :--- |
| af=filename | Specify the filename of the accounting file. |
| br#rate | Specify the data transfer rate for a serial printer. |
| fcl#n | Specify the clear flag bits (n) for a serial printer. |
| ff=string | Assign the form feed string to use with the printer if other than the default (^F). |
| fo | Send a form feed before printing the file. This is a Boolean variable. |
| fsf#n | Specify the set flag bits (n) for a serial printer. |
| if=filename | Specify the filename of an input filter that is started every time a file is printed (*see also of*). |
| lf=filename | Specify the filename of the log file for error messages. |
| lf=filename | Specify the filename of the lock file. |
| ls=filename | Specify the filename of the lock file. |
| lo=device | Specify the device to use as a local printer. |
| mx#n | Set the maximum file size in blocks. Specify *mx#0* for unlimited size. |
| of=filename | Specify the filename of a filter to be applied only at the beginning of a print queue (*see also if*). |
| pc#cost | Specify the cost per page in hundredths of a cent (500 = five U.S. cents). The default is 200. |
| pl#lines | Specify the number of lines per page. The default is 66. |
| pw#width | Specify the minimum page width in characters. The default is 132. |
| px=#width | Specify the page width in pixels. |
| py=#length | Specify the page length in pixels. |
| rg=group | Restrict access to this printer to members of the specified user group. |
| rm=host | Specify the address of the host used for remote printing. Use this option for a LaserJet network adapter. |
| rp=name | Specify the name of the remote printer or printer queue that is accessed with the **rm** command. For PostScript printing with LaserJets, use **rp=raw**. |
| rs | Restrict remote users to those with accounts on this machine. This is a Boolean variable. |
| rw | Enable two-way communication with the printer. This is a Boolean variable. |
| sb | Print a short banner page. This is a Boolean variable. |
| sc | Prevent printing of multiple copies. This is a Boolean variable. |
| sd=directory | Specify the print-spooling directory. |
| sf | Suppress the form feed sent to the printer at the end of the print run. This is a Boolean variable. |
| sh | Prevent printing of the burst page header. This is a Boolean variable. |
| st=filename | Specify the status filename. |
| tr=string | Specify the string to print when the queue is finished. |

## Scheduling Automated Processes with *cron*

The *cron* daemon, installed by default on most Linux distributions, “wakes up” every minute to see whether the system administrator or user has scheduled any jobs for the daemon to run. If so, the daemon runs the requested job (a shell command or script).

The system administrator (root user) can schedule jobs by placing a one-line instruction in /etc/crontab. This instruction consists of a statement containing six fields (see the table “Fields in Crontab Files” in this section), separated by a space, such as the following:

```
0  23  *  *  *  tar  -uf backup.tar  /home/suzanne
```

This command runs the specified tar command at 11 P.M. every evening. In addition to the permitted values listed in the “Fields in Crontab Files” table you can also use an asterisk for fields for which no value is set, a range specified with a hyphen (such as mon-fri), or a comma-separated list of values (such as 5, 7, 9).

If your Linux distribution uses the Vixie cron system, the /etc/crontab file may contain commands such as the following:

```
59  *  *  *  *  root   run-parts /etc/cron.hourly
*  22  *  *  *  root   run-parts /etc/cron.daily
*  23  *  *  sun  root   run-parts /etc/cron.weekly
*  20  *  2  *  root   run-parts /etc/cron.monthly
```

These commands tell cron to run the run-parts script, located by default in /usr/sbin. This script looks in the specified configuration file (such as /etc/cron.hourly) for commands to run at a given interval, such as daily or hourly.

Users can set up their own crontab file, located in their home directory, by running the crontab utility.

### FIELDS IN CRONTAB FILES

| Field | Description |
|---|---|
| 1 | Minute (0 to 59) |
| 2 | Hour (0 to 23) |
| 3 | Day of month (1 to 31) |
| 4 | Month (1 to 12 or the first three letters of the month’s name) |
| 5 | Day (0 to 6, with 0 referring to Sunday, or the first three letters of the day’s name) |
| 6 | Command to execute at the specified time |

### EXAMPLES

| This Command | Does The Following |
| :--- | :--- |
| `59 * * * * rm /home/suzanne /core` | Erases core dump files from the specified directory every hour (at the 59-minute mark). |
| `0 23 * * * tar -uf backup.tar /home/suzanne/documents/* .sdw` | Updates a backup archive every evening at exactly 11 P.M. |
| `0 23 * * mon-fri tar -uf backup.tar /home/suzanne/documents/* .sdw` | Updates a backup archive at 11 P.M. each day of the week, except Saturdays and Sundays. |

## Rotating System Logs

Your Linux system generates a variety of system logs, which record the messages generated by the kernel and various system utilities. One such log is /var/log/messages. Some of these files can grow quite large over time, rendering them difficult to read. If left to grow unchecked, /var/log/messages can grow to many thousands of lines. The logrotate command, discussed in this chapter, keeps these files small by copying all the new messages added since the last rotation to a backup file and then removing this data from the file. This operation is called truncating the file.

A configuration file, generally called /etc/logrotate.conf, enables you to specify how to rotate the system log files. The file begins with global commands (commands that apply to all system log files). A subsequent section contains commands for specific log files. In both sections, you can use the commands listed in the Logrotate Command Options table in this section. Any line beginning with a hash mark (#) is ignored. The following illustrates a typical Global Command section in /etc/logrotate.conf:

```
#Global commands
#Rotate log files daily
daily
#Keep 5 days' worth of backlogs
```
