
purge them. Keep in mind that they do take up a lot of space and need to be moved to another storage area (perhaps to a removable media filesystem), or compressed and retained for a specified time and then removed.

## Task: Managing System Logs

The logrotate command gives you the tools you need to control the disposition of all your system log files. The logrotate command offers a means for emptying out all the data in a logfile and then compressing, rotating, or mailing it. But, before you can use the logrotate command, you must edit the configuration file so that logrotate knows how to rotate system log files.

- 1. Open the `/etc/logrotate.d/syslog` file in your favorite text editor. An example (using the Gedit text editor) is shown in Figure 17.3.

### FIGURE 17.3
The default configuration file for the logrotate command.

![](img/782ecfdc0b083a767896cc983e10427f_276_0.png)

- 2. Tell the system to compress all log files with the gzip command after they are rotated. Create a new line at the top of the file and type `compress` on the blank line. Any commands that appear at the top of the file are applied globally; that is, these commands are applied to every system log file that is listed.

- 3. Tell the system to rotate the `/var/log/messages` log file three times before the oldest copy is deleted. Create a blank line after the line that reads `"/var/log/messages {"` and then type `rotate 3` and press Enter. This is a local command because it only applies to the `/var/log/messages` file.

- 4. Tell the system to rotate the /var/log/messages file monthly. On the blank line you created in step 3, type monthly and press Enter. The /var/log/messages file will be rotated the first time that the logrotate command is executed during a month.

- 5. Tell the system to move the /var/log/messages file to the home directory for the superuser. In the blank you created in step 4, type olddir /root. Your file should now look like the one in Figure 17.4.

### FIGURE 17.4
Proofread your configuration changes before you close the file.

![](img/782ecfdc0b083a767896cc983e10427f_277_0.png)

- 6. Make changes to the other system log files. Table 17.1 shows other commands that you can use to change how these system log files are handled.

### TABLE 17.1 Commands to Tell logrotate How to Rotate Log Files

| Command | Description |
|---|---|
| compress | Compresses old logs with gzip |
| daily | Rotates logs daily |
| delaycompress | Compresses logs on next rotation |
| errors mailto | Mails errors to specified address |
| ifempty | Rotates empty log |
| mail mailto | Mails logs to specified address when deleting |
| monthly | Rotates logs monthly |

### Table 17.1 continued

| Command | Description |
|---|---|
| nocompress | Doesn't compress |
| noolddir | Doesn't move to another directory |
| notifempty | Doesn't compress empty log |
| olddir directory | Moves old logs to specified directory |
| postrotate | Runs script after log is rotated |
| prerotate | Runs script before log is rotated |
| rotate n | Specifies the number of old logs to retain |
| size n | Rotates when log reaches a specified number of bytes (k for kilobytes, m for megabytes) |

- 7. Save the file and close the text editor.
- 8. Run the logrotate command to try out your new configuration changes. At the shell prompt, type `logrotate /etc/logrotate.d/syslog` and press Enter.

Now when you go back to the /var/log directory, you'll see several files for the messages system log file. All the files will be compressed. As the messages logs are rotated, the new log becomes messages, the current log is saved as messages.1, old messages.1 becomes messages.2, and so on.

![](img/782ecfdc0b083a767896cc983e10427f_278_0.png)

## Creating a Comfortable Work Environment

Not only are safe work environments regulated by the Occupational Safety & Health Administration (OSHA), but they are essential in maintaining a productive and happy workforce. Even if you run a small business out of your garage, you must still ensure the health and safety of your most valuable employee—you! It might be a good idea to insure yourself also, so be sure and get a good policy.

According to the Bureau of Labor Statistics, musculoskeletal disorders (MSDs) represent one-third of the work-related injuries and illnesses in the United States. MSDs are caused by repetition, poor posture, lack of movement, force, vibration, and cold temperatures. OSHA encourages all employers to implement ergonomic programs; learn how at www.osha-slc.gov/SLTC/ergonomics. If you are curious about the standards being developed by OSHA, read the FAQ at www.osha-slc.gov/ergonomics-standard/faq-overview.html.

A large number of MSDs are caused by long periods spent at the computer. If you'd like to prevent some of the repetitive strain injuries suffered by old-time computer users, experiment with a few ergonomic techniques. You might want to look up Ergoworld (at www.interface-analysis.com/ergoworld). Ergoworld contains links to about every ergonomic, repetitive strain injury, and injury prevention Web site in cyberspace.

The easiest ways to prevent computer-related injuries are to sit up straight to avoid fatigue and back problems, learn keyboard commands and short-cuts to reduce repetitive strain injuries caused by the mouse, and walk away from the computer regularly to delay burnout.

## Task: Using cron to Rotate System Logs Automatically

Now that you've set up a system for rotating system logs, you might want to have the computer do this automatically. In this task, you will use cron to run the log rotation command at 6:50 p.m. on the 1st and 15th of every month.

- 1. Decide when you want cron to run the log rotation. Figure 17.5 shows how the information should be arranged in the file.

### FIGURE 17.5
Use acceptable values to fill in each field.

![](img/782ecfdc0b083a767896cc983e10427f_279_0.png)

- 2. Open a new file called rotatelogs in your favorite text editor and store it in your home directory.

- 3. In the text editor, type the following:

```
50 18 1,15 * logrotate /etc/logrotate.d/syslog
```

The third field (1,15) shows the command running on the 1st and 15th day of the month. You can use a comma to separate several values within a single field.

The fourth field (*) tells the command to run this command every month. When you want the field to contain all possible values, use the asterisk (*) character.

The fifth field is empty (indicated by a blank space) showing that the command is not dependent on running on a certain day of the week.

The sixth field is the command that is to be executed based on the time set in the first five fields.

- 4. Save and close the file.
- 5. Set up the file so that it is recognized by the cron daemon. Type `crontab rotatelogs` and press Enter.
- 6. View your crontab file. Type `crontab -l` and press Enter. The crontab listing appears in Listing 17.2.

### LISTING 17.2 The crontab Entry

```
[root@localhost root]# crontab -l
# DO NOT EDIT THIS FILE - edit the master and reinstall.
# (rotatelogs installed on Mon Jul 10 22:44:12 2000)
# (Cron version — $Id: crontab.c,v 2.13 1994/01/17 03:20:37 vixie Exp $)
50 18 1,15 * * logrotate /etc/logrotate.d/syslog
[root@localhost root]#
```

- 7. View the crontab listing. There should be a file in the /var/spool/cron directory that uses your username as the filename. For example, because the superuser created this crontab entry, the file would be located at /var/spool/cron/root.

After this file is set up, you don’t have to do anything else to make sure that the logs are rotated according to your needs. You can create other crontab entries using this same procedure. Any other crontab entries that you make will be added to your file in the /var/spool/cron directory.

## Summary

During this past hour, you learned how to perform some basic system administration tasks to help reduce the storage load on your hard drive. You then learned how to automate this task using the cron daemon. This hour explored just a few of the ways that you can increase hard drive space and automate routine system tasks. As you learn more about your Linux system, you’ll find many more ways to automate routine tasks.
