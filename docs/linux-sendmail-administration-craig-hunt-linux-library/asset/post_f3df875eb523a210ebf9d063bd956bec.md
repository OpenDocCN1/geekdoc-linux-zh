
# On a BSD-Style Linux System

Linux systems like Slack that use BSD-style boot procedures start Sendmail by executing the sendmail command directly from one of the main start-up files. The code that runs the Sendmail daemon in the Slackware Linux /etc/rc.d/rc.M start script is very straightforward, as shown in Listing 3.1.

## Listing 3.1 Starting Sendmail from a Slackware Boot Script

```bash
# Start the sendmail daemon:
if [ -x /usr/sbin/sendmail ]; then
    echo "Starting sendmail daemon"
    /usr/sbin/sendmail -bd -q 15m
fi
```

Listing 3.1 shows a Slackware system ready to run Sendmail. The first line is a comment, as indicated by the fact that it starts with a pound sign (#). The next lines are an if statement checks whether or not the sendmail command is available. If the command found a message is displayed on the console indicating that Sendmail is starting and then the sendmail command runs.

The code in Listing 3.1 runs the sendmail command with the -bd and -q options. In addition to listening for inbound mail, the Sendmail daemon periodically checks to see whether there is mail being delivered. It's possible that a Sendmail process that started to send a message was not able to successfully deliver the mail. In that case, the process writes the message to the mail queue and counts on the daemon to deliver it at a later time. The -q option tells the Sendmail daemon how often to check the delivered mail queue. In the Slackware example, the queue is processed every 15 minutes (-q15m).

To prevent Slackware from starting at boot time, the lines shown in Listing 3.1 out of the rc.M script by placing a pound sign at the beginning of each line. To restore Sendmail to the boot process, remove the pound signs. These techniques are easy and they work, but they are far from elegant.

Direct editing a start-up script is easy, but dangerous. Most system administrators worry that an editing error will have a major negative impact on the next boot. I have never really had a major boot problem cause by an editing error, but I understand the fear. Distributions that use V-style start-up procedures alleviate this fear by making it unnecessary to directly edit the start-up file.

# On a System V–Style Linux System

Most distributions use a System V–style boot process that allows the system to be initialized in different ways depending on the runlevel. All of the service initialization scripts are contained in a single directory, usually `/etc/rc.d/init.d` on Linux systems that use this style of start-up. The initialization scripts are indirectly invoked by links contained in directories assigned to each runlevel. Caldera and Red Hat are good examples of System V–style Linux systems.

> NOTE A detailed description of the Linux boot process is beyond the scope of this book. To learn more about the boot process, runlevels, and start-up scripts, see Linux Network Servers 24seven by Craig Hunt (Sytex, 1999).

The code that Caldera and Red Hat use to start the sendmail daemon is found in the `/etc/rc.d/init.d/sendmail` script. It is more complex than the code used by Slackware, because Red Hat and Caldera use variables read from an external file to set the command-line options. The file they read is `/etc/sysconfig/sendmail`, which normally contains these two lines:

```
DAEMON=yes
QUEUE=1h
```

Changing the values in the `/etc/sysconfig/sendmail` file controls the daemon configuration. The QUEUE variable sets the time value of the -q option. In this case, it is one hour (1h), which is a value I like even more than the 15 minutes used by Slackware configuration. Processing the queue too often can cause problems if the queue grows very large due to a delivery problem such as a network outage.

If the variable DAEMON is equal to "yes," the sendmail command run with the -bd option. If you are configuring a mail client and do not want to run Sendmail as a daemon, you could directly edit the `/etc/sysconfig/sendmail` file to set DAEMON=no.

> TIP While changing the DAEMON value is one to do this, it is generally a better idea to remove the sendmail script from the start-up as described below than it is to edit the contents of a script.

With System V–style start-up, you don't have to directly edit start-up files. One of the advantages of the System V–style boot procedure is that major services have their own start-up scripts and those scripts are indirectly invoked, which makes it possible to control whether or not a service is started at boot by controlling whether or not the script invoked. The sendmail script is invoked indirectly from the runlevel directories by the S80sendmail script (see Listing 3.2). An examination of that script shows that it is just a symbolic link to the real sendmail script.

## Listing 3.2 The Sendmail Link for Runlevel 3

```bash
[crag]$ cd /etc/rc.d/rc.3
[crag]$ ls -1 S80sendmail
1rw-xr-x 1 root root 02 26 1999 S80sendmail -> ../init.d/sendmail
```

To enable or disable the sendmail start-up for a specific runlevel, simply add or remove the symbolic link in that runlevel's directory. And of itself this would be simple enough, but Linux systems make it even easier by providing tools to manage the runlevel directories.

# Enabling Sendmail with tksysv

tksysv is an X Windows tool for the purpose of controlling scripts started at each runlevel. Figure 3.1 shows the main tksysv screen.

## Figure 3.1 Enabling Sendmail with tksysv

| SYSV Runlevel Manager, v0.92 | | | | |
| Available: | 2 | 3 | 4 | 5 |
|---|---|---|---|---|
| routed | | keytable | nfs | autofs |
| rstats | network | sendmail | autofs | keytable |
| rusersd | random | keytable | sendmail | gpm |
| rwhod | t sound | httpd | httpd | |
| sendmail | a crowd | sound | sound | xfs |
| single | r pcmia | vmware | xfs | smb |
| smb | l | | | linuxconf |
| syslog | keytable | linuxconf | linuxconf | |
| vm | gno | local | | |
| xfs | | | | |
| yphbind | autofs | rstats | rstats | rstats |
| ypasswdd | sound | rusersd | rusersd | rusersd |
| ypserv | httpd | rwhod | rwhod | rwhod |
| Add | nfs | ypasswdd | ypasswdd | ypasswdd |
| Remove | t rstatsd | dhcpd | dhcpd | dhcpd |
| Edit | e rusersd | named | named | named.rmpc |
| Execute | rwhod | routed | routed | routed |
| | sendmail | ypserv | ypserv | | |
| | ypasswdd | yphbind | | |

# Chapter 3 Running Sendmail

All of the scripts that can be controlled by tksysv are listed on the left-hand side of the screen. On the right are the services that are started and stopped for runlevels 2, 3, 4, and 5. To disable a service for a specific runlevel, simply highlight the service in the Start list for that runlevel and click the Remove button. For example, remove Sendmail from runlevel 5, which is traditionally used for the dedicated X workstations, click sendmail in the Start list under runlevel 5 and click Remove. After that, Sendmail will no longer start when the system boots under runlevel 5.

To add Sendmail to a runlevel, highlight sendmail in the Available list and click Add. Youll be asked to select a runlevel. An example might be runlevel 3, which is traditionally the default runlevel for multiuser servers. Select the runlevel and click Done. You're asked to select a script name. Use the default, which is 80 for the sendmail script. Click Add and the script is added to the start-up. The next time the system reboots under runlevel 3, Sendmail will be started.

> TIP If you don't want to reboot your system just to run the sendmail start-up. Use the Execute button to run the sendmail script immediately.

tksysv has a couple of nice features. First, it comes bundled with different versions of Linux. It runs just as well on Caldera as it does on Red Hat, and it runs just as well as under Red Hat 6 as it does under Red Hat 7. Second, a clone of tksysv called nsysv runs in text mode and therefore doesn't require X Windows. A dedicated e-mail server might not be running X Windows. In that case, you want a tool like nsysv that runs in text mode.
