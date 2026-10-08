
5. Arrange for PortSentry to be invoked. My preferred method is to add the following to /etc/rc.d/rc.local. If it is already running, it will be killed and restarted for ease of use when tweaking the portsentry.conf file:

```
echo "Starting portsentry advanced stealth modes"
killall portsentry
# Generate list of IPs to ignore scans from
# (friends from /etc/rc.d/friends.ignore)
/usr/local/psionic/portsentry/ignore.csh
# Advanced stealth TCP
/usr/local/psionic/portsentry/portsentry -atcp
# Advanced stealth UDP
/usr/local/psionic/portsentry/portsentry -audp
```

Start PortSentry with the command:

```
/etc/rc.d/rc.local
```

and monitor:

```
tail -20f /var/log/messages
```

6. Test the configuration. From an untrusted system (and one which is not your only way to access the system under test), telnet to an alarmed port:

```
telnet firewall 6000
```

Observe that an entry has been added to /var/log/messages and that a new IP Tables rule has been added by issuing the command:

```
iptables -L -n -v | more
```

## HostSentry

The HostSentry program analyzes login patterns and reports abnormalities, including users logging in for the first time, users logging in at unusual times (for them), and users logging in remotely from unexpected domains. It is available from the CD-ROM and from Psionic.

This URL may be used for downloading and provides more explanation of HostSentry's capabilities.

www.psionic.com/abacus/hostsentry/

## 8.6 Paging the SysAdmin: Cracking in Progress!

Although the methods just discussed are very quick and easy to set up, a whole lot of damage can be done by the time you check your e-mail the next day or possibly not until after Monday 9 A.M. meeting! You can combine some of syslog's features that are available in the /etc/syslog.conf file for immediate warnings of problems. The simplest feature is specifying accounts in the action field so that the warning message will be written to anyone the named people are logged in on.

Typically, the SysAdmins' personal accounts as well as root will be listed. This is coarse and does not allow any intelligent filtering or warnings. You can be even coarser with an action of `""`, which will cause the warning message to be displayed on everyone's logged-in screen, including the cracker's. This might be appropriate for warnings about running out of disk space; this generally is not done.

Under Linux you can write specified messages to one or more named pipes where you can have your intelligent filtering program listening. This is done by prepending `|` to the named pipe's full pathname without a separating space. The named pipe must exist and the listener must be running prior to syslog starting.

The listener can arrange for you to be paged. Tel pagers and most others have a feature where e-mail sent to a particular address gets routed to a pager. The e-mail address might be `1234567@skytel.com`, where `1234567` would be the pager number.

This e-mail service is free from Sky Tel but must be activated before use. When activating the service you will need to specify which of the following fields get sent to your pager: `from`, `subject`, and `body`. Selecting all of these fields will cause some messages to exceed the message length limit. Response time typically is about five minutes.

Some other paging companies may offer automated paging by having your modem dial into theirs and supplying a message or via e-mail.

## 8.7 An Example for Automatic Paging

For this example, you will arrange to be paged on unsuccessful telnet login attempts. The only entry in your /etc/syslog.conf that has an action of displaying on logged-in users' screens is:

```
*.warn,authpriv.notice,auth.notice bob,root
```

and it generates the following (on a single line):

```
Nov 22 22:07:37 cavu login[24072]: invalid password for `UNKNOWN` on `ttypp6` from `359`
```

Unfortunately, there is no documentation or simple way to determine which facet (before the `: `) telnetd is using to generate this message. It is suggested that you edit the /etc/syslog.conf file, copy this line, comment out the original, edit the copy to specify only some of the selectors, and force the message to be generated to see if it appears.

The telnetd daemon says "UNKNOWN" if the person entered an account name that is not in /etc/passwd; otherwise it will list the account name, as "bob". You might modify your telnetd so that instead of saying "UNKNOWN" it will say "U-joe" so if they are trying to guess account names you will see "U-joe", "U-joe", "U-jane", "U-jane", etc. and assume that they are trying a few unlikely passwords on common account names. Note that you must separate the selectors from the accounts with tabs, no spaces.

```
authpriv.notice  bob
```

I then did:

```
ps axlww | grep syslog
```

to find the PID (97 in my case) for syslog and then sent it the HUP signal to reread the /etc/syslog.conf file thus:

```
kill -HUP 97
```

I tried to telnet in with a bogus login sequence but I did not see the login message so this is the wrong selector.

I tried:

```
auth.notice  bob
```

(and sent the `kill -HUP 97` and tried to telnet in. This generated the message so this is the selector to use. You first need to create a shell script (or Perl or C program) to transform this error message to an appropriate Mail command to activate the pager. Due to a limited pager message length, you want to edit the message.

The following script does the job. It may be invoked from any shell. It could be named /usr/local/bin/syslog_login.

```
#!/bin/csh -f
loop:
set x="$<"
echo "$x" | grep -q ': invalid password'
if ($status == 0) then
echo "$x" | sed 's/^.*: \([^ ]*\): invalid password for /BAD PW:\1:/' | mail 1234567@skytel.com
endif
goto loop
```

This will cause the following to appear on your pager once you put this feature into operation. This shows what your system is using for telnet so you know how alarmed to be.

```
BAD PW:cavu:'bob' on 'ttypp6' from 'cavu'
```

Because your pager will indicate the time of the page, do not clutter the screen with a time-stamp. Next you need to create the named pipe that will convey the data from syslog to this script. This pipe only needs to be created as root thus:

```
mknod /usr/local/etc/syslog_auth p
chmod 600 /usr/local/etc/syslog_auth
```

Next, you need to arrange for this script to be started on system startup. In Red Hat or Slack, you could add the following line to the /etc/rc.d/rc.local file:

```
(/usr/local/bin/syslog_login </usr/local/etc/syslog_auth) &
```

You then want to start this the first time by issuing the command to a root shell or simply by rebooting if that would not be inconvenient.

> Note that it is important when making any alteration to the boot sequence, including altering startup scripts, creating a new kernel, etc., that you have an easy alternate to reboot the system and undo your changes in case you make a mistake that renders the system unbootable.

Usually this involves a set of rescue disks. Normally, these are created after major updates. They consist of a copy of your kernel (patched with rdev to detect the root file system on floppy) and a compressed image of a suitable rescue root system. The root file system floppy can be copied with `dd` from your Linux distribution CD-ROM. The procedure for all of this is described in the Linux Administrator's Documentation.

Finally, you need to alter that entry in /etc/syslog.conf to read:

```
auth.notice |/usr/local/etc/syslog_auth
```

and then use `kill` to send a SIGHUP to syslogd. Now you are ready to test this by trying to telnet in with a bogus password or login ID.

## 8.8 Building on Your Example for Automatic Paging

You wrote your script in that particular way because it allows you to easily scan for other events and generate custom pages for them. In a large system, some people will have weak passwords (unless you ensure easily cracked passwords are not allowed as discussed in Part 1).

Thus, a common technique is to guess the password of some ordinary user as the first step in breaking in, followed by trying to `su` to root (Part 1 discusses how to configure your system so that root may log in from a physically secure console and not via telnet somewhere in crackdoom).

Certainly, you will want to be paged in case of failed `su` attempts. The program also logs failed attempts via `auth.notice`. Thus, simply add a few lines to your script and restart.

```
#!/bin/bash -f
while true
do
    read x
    echo "$x" | grep -q ': invalid password'
    if [ $? -eq 0 ]; then
        echo "$x" | sed 's/^.*: \([^ ]*\): invalid password for /BAD PW:\1:/' | mail 12345667@skytel.com
    fi
    echo "$x" | grep -q 'su\[.*\]: Authentication failed'
    if [ $? -eq 0 ]; then
        echo "$x" | sed 's/^.*: \([^ ]*\): Authentication failed for /BAD SU:\1:/' | mail 12345667@skytel.com
    fi
done
```

This will yield the following page on an unsuccessful `su` to root:

```
BAD SU:cavu:root
```

You did not need to send a HUP because its configuration file has not changed.

This second example principally shows how to add handling for other messages to a single script. It would be helpful to know which account attempted to `su` to root and on which terminal, so you do not get disturbed if your assistant is tweaking the system some evening.

The `su` program does log this additional information, but at the debug level. Because lots of other programs log security-related information at this level, send all of them through your script and pick which messages to page on. Thus, edit /etc/syslog.conf to show the following and send a SIGHUP to syslog:
