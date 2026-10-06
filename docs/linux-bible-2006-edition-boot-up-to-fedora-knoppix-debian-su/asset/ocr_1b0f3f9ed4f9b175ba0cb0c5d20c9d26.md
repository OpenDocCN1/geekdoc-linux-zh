# 140 Part II ♦ Running the Show

If you are using Red Hat Linux system, the System Logs utility is a good way to step through your system's log files. From the red hat menu, select Applications-> System Logs. You can not only view boot, kernel, mail, security, and other system logs, but you can also use the filter box to search for particular terms (such as a model number of a piece of hardware that's not working).

On SUSE systems, you can view log files from YaST. For example, select Miscellaneous and then choose View System Log or Start-Up Log to view the messages or boot.msg files, respectively.

# Using sudo and Other Administrative Logins

You don't hear much about administrative logins (besides root) being used with Linux. It was a common practice in UNIX systems to have several different administrative logins that allowed administrative tasks to be split among users. For example, a person sitting near a printer could have ip permissions to move jobs to another printer if he knew a printer wasn't working.

In any case, administrative logins are available with Linux, so you may want to look into using them. Here are some examples:

+   * **lp**—Can control printing features. Having a separate ip allows someone other than the superuser to do such things as move or remove logs and print spool files. The home directory for it is /var/spool/lpd.

+   * **mail**—Can use with administrative email features. The mail group, for many Linux systems, has group permissions to use mail files in /var/spool/mail (which is also the mail user's home directory).

+   * **uccp**—User owns various u commands (once used as the primary method for dial-up serial communications) as well as log files in /var/log/uccp, spool files in /var/spool, administrative commands (such as uuchk, uucico, uconv, and uucqt) in /usr/sbin. The home directory for uccp is /var/spool/uccp.

+   * **news**—Could do administration of Internet news services, depending on how you set permission for /var/spool/news and other news-related resources. The home directory for news is /etc/news.

One way to give or limited root privileges to nonroot user is to use the sudo facility, which simply entails adding the user to /etc/sudoers and defining what privilege you want that to have. Then the user can run any command or she is privileged to use by preceding that command with the sudo command.