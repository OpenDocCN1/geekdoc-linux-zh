look strange, but there is a consistent naming scheme. The first two characters indicate what type of data is stored in the file (as described in Table 19-1). All subsequent characters form a unique random identifier based on the PID of the sendmail process that is handling that message.

# Table 19-1: File Prefixes in /var/spool/mqueue

| Filename Prefix | Type of Data Stored |
| --- | --- |
| df | The data that constitutes the body of an e-mail message. |
| qf | The queue control file that contains the message headers and other administrative details. |
| tf | A temporary copy of the qf file, created if delivery errors are encountered. |
| xf | Any error messages generated while attempting to send the message. |

# Other programs

As indicated in the output from the sendmail installation, several other executable programs are included in the distribution. These are described in Table 19-2.

# Table 19-2: Other Related Sendmail Programs

| Program | Description |
| --- | --- |
| hoststat | Displays the status of hosts that have recently communicated with the sendmail daemon on the local machine. The command is equivalent to sendmail -bh, which is not enabled by default. |
| mailq | Displays a summary of the messages awaiting processing in the mail queue (the command is equivalent to sendmail -bp). |
| mailstats | Displays message quantity and byte count statistics. |
| makemap | Translates a plain-text file (i.e., /etc/mail/virtualuser table) into a hashed Berkeley database file (i.e., /etc/mail/virtualuser table.db). This command runs each time the sendmail script starts at boot time. |
| newaliases | Translates the plain-text /etc/aliases file into the hashed Berkeley database file /etc/aliases.db (the command is equivalent to sendmail -bi). |
| praliases | Prints out all aliases defined in /etc/aliases. |
| procmail | Not included with the sendmail package, but is used as an MDA for sendmail. |