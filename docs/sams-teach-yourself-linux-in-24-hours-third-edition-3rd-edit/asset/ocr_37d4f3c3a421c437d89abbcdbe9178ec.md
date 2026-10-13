4. Tell the system to rotate the /var/log/messages file monthly. On the blank line you created in step 3, type monthly and press Enter. The /var/log/messages file will be rotated the first time that the logrotate command is executed during a month.

5. Tell the system to move the /var/log/messages file to the home directory for the superuser. In the blank you created in step 4, type olddir /root. Your file should now look like the one in Figure 17.4.

# FIGURE 17.4 Proof your configuration changes before you close the file.

![](bbox=[0.38, 0.4, 0.8, 0.78])

6. Make changes to the other system log files. Table 17.1 shows other commands that you can use to change how these system log files are handled.

# TABLE 17.1 Commands to Tell logrotate How to Rotate Log Files

| Command | Description |
|---|---|
| compress | Compresses old logs with gzip |
| daily | Rotates logs daily |
| delaycompress | Compresses logs on next rotation |
| errors mailto | Mails errors to specified address |
| ifempty | Rotates empty log |
| mail mailto | Mails logs to specified address when deleting |
| monthly | Rotates logs monthly |