The fax shell script converts the PostScript graphic to fax format and sends it to the remote fax (albeit in black and white, not color).

To set your computer to automatically wait for incoming faxes, you can use the fax script's wait command-line option, for example:

```
# fax wait
running /usr/bin/fax answer
/usr/bin/efax: Tue Dec 29 22:38:02 1998 efax v 0.8a Copyright
© 1996 Ed Casas
```

You can also use the background operator to put the shell script in the background. You can check on the status of your Linux fax machine with the status command-line option, for example:

```
# fax status
USER PID %CPU %MEM SIZE RSS TTY STAT START TIME COMMAND
root 785 1.8 0.6 1032 404 p2 S < 21:45 0:00 /usr/bin/efax -d/dev/
from: /var/spool/fax/modem.785
efax: 45:23 opened /dev/modem
efax: 45:25 waiting for activity
```

This shows that the efax command is waiting on the /dev/modem serial port for incoming faxes. To check whether you've received any faxes, you can use the fax command's queue command-line option, for example:

```
# fax queue

Fax files in /var/spool/fax :

-rw-r--r-- 1 root root 18449 Dec 29 21:51 1229215055.001
-rw-r--r-- 1 root root 15001 Dec 29 21:54 1229215350.001
-rw-r--r-- 1 root root 16229 Dec 29 21:54 1229215350.002
```

This output shows that two faxes have been received. The first is a one-page fax received at 9:51 p.m. The other is a two-page fax received three minutes later. These faxes are waiting in the /var/spool/fax directory (created automatically when you first run the fax command with the wait command-line option). Each page of a fax is saved as a separate file, and pages of the same fax have the same filename with the date and time, followed by the page number as an extension.

To view a fax, you can use the fax command's view option. For example, to view the one-page fax, as shown in Figure 9.8, use the fax command with the view option, followed by the fax's filename, like this:

```
# fax view 1229215305.001
/var/spool/fax/1229215055.001
1229215055.001 ...
```