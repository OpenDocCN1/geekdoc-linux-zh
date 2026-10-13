+   2. Log in properly with the correct password as the root user.
+   3. In a console, navigate to the /var/log directory and open the file named secure. Navigate to the "FAILED LOGON" message closest to the end of the file. Close the file.
+   4. Review other logs in the /var/log directory. Use Table 9-7 for guidance. Look for messages associated with hardware. What log files are they in? Does that make sense?
+   5. Most, but not all log files are text files. Try reading the lastlog file in the /var/log directory as a text file. What happens? Try the lastlog command. Are you now reading the contents of the /var/log/lastlog file? Can you confirm this from the associated man page?

# SCENARIO & SOLUTION

| Problem | Solution |
|---|---|
| Can't connect to a local VNC server | Make sure the VNC server is running with the `/etc/init.d/vncserver restart` or `vino-preferences` command. |
| Can't connect to a remote VNC server | Make sure you're connecting to the right port; for example, a connection to 192.168.100.1:1 requires open ports 5900 and 5901. Review open ports with appropriate `nmap` and `telnet` commands. |
| Regular users can't access the crontab command or the at prompt | Review the cron.allow and cron.deny files in the /etc/ directory. If all regular users are allowed access, make sure the cron.deny file exists but is empty and to delete cron.allow. (Similar guidelines apply for the at prompt.) |
| Log files don't include sufficient information | Revise `/etc/rsyslog.conf`. Focus on the desired facility such as authpriv, mail, or cron, and revise the priority to include more detailed information |