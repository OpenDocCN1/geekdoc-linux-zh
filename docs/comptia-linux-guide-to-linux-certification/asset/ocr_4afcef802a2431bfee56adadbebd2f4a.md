+   2. At the command prompt, type `ls -1 /dev/log` and press **Enter**. What is the file type? Which daemon on Ubuntu Server Linux uses this file and what is its purpose?

+   3. At the command prompt, type `less /etc/rsyslog.conf` and press **Enter** to view the configuration file for the System Log Daemon. Are there any entries that specify facilities, priorities, or log file locations? What does the last line of the file specify? Press **q** when finished to quit the less utility.

+   4. At the command prompt, type `less /etc/rsyslog.d/50-default.conf` and press **Enter**. Where do kernel messages of any priority get logged to by default? What does the `–` character next to the filename indicate? Press **q** when finished to quit the less utility.

+   5. At the command prompt, type `tail /var/log/kern.log` and press **Enter**. Observe the entries.

+   6. At the command prompt, type `ls /var/log/cups` and press **Enter**. What daemon creates the log files within the /var/log/cups directory?

+   7. At the command prompt, type `cat /etc/cron.daily/logrotate` and press **Enter** to observe the `logrotate` command that is run each day.

+   8. At the command prompt, type `less /etc/logrotate.conf` and press **Enter** to view the configuration file for the `logrotate` command. How many copies of old log files are kept by default? When finished, press **q** to quit the less utility.

+   9. At the command prompt, type `ls /etc/logrotate.d` and press **Enter**. How many files are in this directory? Will entries in these files override the same entries in `/etc/logrotate.conf`?

+   10. At the command prompt, type `cat /etc/logrotate.d/cups-daemon` and press **Enter**. How many copies of old log files are kept for the log files in the /var/log/cups directory? Will the log files be rotated if they contain no contents?

+   11. Type `exit` and press **Enter** to log out of your shell.

# Project 10-4

In this hands-on project, you view the configuration and log entries created by the Systemd Journal Daemon as well as the configuration of the logrotate utility on Fedora Linux.

+   1. On your Fedora Linux virtual machine, switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2** and log in to the terminal using the user name of `root` and the password of `LNXRocks!`.

+   2. At the command prompt, type `ls -1 /dev/log` and press **Enter**. What is the file type? Which daemon on Fedora Linux uses this file and what is its purpose?

+   3. At the command prompt, type `cat /etc/systemd/journald.conf` and press **Enter** to view the configuration file for the Systemd Journal Daemon. What line could you uncomment and configure to set a maximum size for the journal database?

+   4. At the command prompt, type `journalctl _COMM=` and press the Tab key twice. Which keyword could you use to view log entries from the GNOME display manager? Press **Ctrl+c** to return to your command prompt. Next, type `journalctl _COMM=gnome` and press **Enter** to view log entries from the GNOME display manager. Are entries shown for multiple days?