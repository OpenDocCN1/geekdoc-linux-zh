the **su(1M)** command to become the superuser. You can monitor and log the use of the **su** command in several ways. The /etc/default/su file controls this monitoring and logging.

To display use of the **su** command on the system console, add the following entry to the /etc/default/su file:

```
CONSOLE=/dev/console
```

Both failed and successful attempts to use the **su** command are displayed on the console. By default, the use of the **su** command is not displayed on the console. To enable this feature, edit the /etc/default/su file and remove the shell comment character (#) at the beginning of the entry. Note that this entry is identical to the entry used in the /etc/default/login file to restrict root login to the system console.

The following examples show the messages displayed on the console for two uses of the **su** command. The first shows an unsuccessful attempt to become root on the system named solaris8 from the login dla. The second shows a successful attempt to become the root. The messages beginning with a date are displayed regardless of the CONSOLE entry in the /etc/default/su file. The message beginning with **SU** is displayed because the CONSOLE entry in the /etc/default/su file is uncommented:

```
Mar 29 02:46:01 solaris8 su: 'su root' failed for dla
on /dev/pts/5

SU 03/29 02:49 + pts/5 dla-root
Mar 29 02:49:16 solaris8 su: 'su root' succeeded for dla
on /dev/pts/5
```

The use of the **su** command can be logged to a file dedicated for **su** logging by adding the following entry in the /etc/default/su file (although the default is shown here, you can use any file for the sulog):

```
SULOG=/var/adm/sulog
```

Both failed and successful attempts to use the **su** command are logged. By default, use of the **su** command is logged to the sulog. To disable this feature, edit the /etc/default/su file and add the shell comment character (#) at the beginning of the entry.

The following lines show the contents of a /var/adm/sulog file:

```
SU 03/18 01:46 + console root-daemon
SU 03/22 00:58 + pts/5 dla-root
SU 03/29 02:42 + pts/5 dla-guest
SU 03/29 02:43 + pts/5 dla-root
SU 03/29 02:46 - pts/5 dla-root
SU 03/29 02:49 + pts/5 dla-root
```