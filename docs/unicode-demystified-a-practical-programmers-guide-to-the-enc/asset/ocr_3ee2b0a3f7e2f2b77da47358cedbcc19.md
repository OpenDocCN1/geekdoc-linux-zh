Replace pid with the process ID of the suspect process; iot displays a list of all file descriptors that process n has open. The -s option displays the size of all open files. The size information may be helpful in determining whether the process has a very large file open. If so, contact the owner of the process, or if necessary, call the process. The -n option redisplays the output of iot every n seconds.

# Keeping a Machine Log

A machine log that includes the information shown in Table 17-24 can help you find and system problems. Note the time and date for each entry in the log. Avoid the temptation to keep the log only on the computer because it will be most useful to you at times when the machine is down. Another good idea is to keep a record of all e-mail about user problems. One way to do this is to save all this to a separate file or folder as Another way is to set up a special alias that users send when they have problems. This alias can then forward mail to you and also store a copy in an archive file. Following is an example of an entry in the /etc/aliases file that sets this type of alias:

```
trouble: admin,/var/mail/admin.archive
```

E-mail sent to the trouble alias will be forwarded to the admin user and also stored in the file /var/mail/admin.archive. Remember to run the newaliases after editing /etc/aliases.

| Condition | table 17-24 |
|---|---|n| Hardware modifications | Keep track of the system hardware configuration: which interrupt is used for which device, what I/O addresses are needed by which card, which devices hold which partitions, and so on.n System software modifications | Keep track of the options used by Linux. Print such files as /usr/include/linux/autoconf.h (Linux kernel configuration), /etc/modules.conf, and /etc/X11/X86Config (X11 configuration). The file hierarchy under /etc/sysconfig contains valuable information about network configuration and so on.n| Hardware malfunctions | Keep as accurate a list as possible of any problems with the system. Make note of any error messages or numbers that the system displays on the system console and what users were doing when the problem occurred.
| User complaints | Make a list of all reasonable complaints made by knowledgeable users (for example, "machine is abnormally slow").|