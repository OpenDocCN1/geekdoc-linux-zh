the other hand, runs the entire time the system is running, constantly listening for inbound mail and periodically processing the queue to deliver undelivered mail. The Sendmail daemon, like most other daemons, is started at boot time.

the ps command reveals whether or not Sendmail is running on your system:

```
ps -C sendmail
PID TTY      TIME CMD
542 ?       00:00:36 sendmail
```

The low process ID (PID) shows that this process was started during the boot. Running this ps command on Linux systems will show that Sendmail is running because, generally, Sendmail becomes part of the boot process when you first install Linux.

Many systems are running the Sendmail daemon unnecessarily. It is not necessary to run Sendmail as a daemon in order to send mail. The sendmail command with the -bd option is required only if your system directly receives SMTP mail. A Linux mail client can collect inbound mail from the mailbox server using POP or IMAP and relay outbound mail through the mail relay server without running the Sendmail daemon. Deciding which systems should run the Sendmail daemon is part of planning your e-mail architecture. Unneeded daemon consumes system resources and provides holes through which network intruders can slash. Take care when selecting systems really need any daemon, including Sendmail.

It is possible to enable or disable Sendmail after the system is installed, and there are several tools to do this. These tools vary depending on the type of start-up procedures used. Some Linux systems use BSD-style start-up procedures, while others use V-style procedures.

On distributions that use V-style boot procedures, the script that starts Sendmail is usually found in the /etc/rc.dinit directory, where it is stored under a name such as sendmail, mail, or mta. On distributions that use BSD-style boot procedures, the commands that start Sendmail are found in one of the rc.m script located in the /etc/rc.d directory. Regardless of the name of the script used for this purpose, some start-up script is used to start Sendmail at boot time.

> TIP Locate the daemon start-up script on your Linux system, go to the directory that holds start-up scripts and run the command grep sendmail * to search every file for references to Sendmail. Not sure where the start-up scripts are stored? Go to /etc and look for files or directories that begin with the string rc. Those are start-up files and directories.