Examples for the Users in INTERNS Let's first see what happens when the user paul tries to restart the printer daemons without using sudo. Example 9-5 displays the output of this attempt. Paul does not have the necessary permissions to kill and restart the lpq daemon, because it is owned by root. Since Paul has been granted permissions to do this in the /etc/sudoers file, he can accomplish his task by using sudo. Example 9-6 shows the user paul restarting the printer daemons using sudo. When sudo is executed for the first time, it displays the lecture message and then prompts paul for his password. At this point, paul may execute additional sudo commands without the lecture and password prompt for up to 5 minutes. Paul can extend this time limitation by using sudo -v. Even this command will require a password if the 5-minute limitation has lapsed.

# Example 9-5 Insufficient Permissions to Restart lpq

```
```
[paul@fohgnrn]$ /usr/sbin/lpc restart all
lp:
/usr/sbin/lpc: connect: Permission denied
[paul@fohgnrn]$ 
```
```

# Example 9-6 Successful lpq Restart Using sudo

```
```
[paul@fohgnrn]$ sudo /usr/sbin/lpc restart all
We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these two things:

#1) Respect the privacy of others.
#2) Think before you type.
Password: paul's password
lpq:
daemon aborted
lpq:
daemon started
[paul@fohgnrn]$ 
```
```

Suppose that Paul needs to reboot the system. Based on the /etc/sudoers file, he is allowed to execute /sbin/shutdown -r. Let's see what happens in Example 9-7 if he executes the shutdown command without the -r flag. At this point, Paul is uncertain about why he can't reboot the system. After all, Mary told him that he had the permission to do that. So Paul decides to see what privileges he actually has by executing sudo -1, as shown in Example 9-8. The output of this command informs Paul that he may execute only shutdown -r (just like Mary said). Notice that it also informs him that he may run all commands in /usr/local/db/bin/, as well as the commands /usr/sbin/lpc and /usr/bin/lprm as either the root or dcmgr users. However, he cannot

# Example 9-7 Failed sudo Execution Due to Incorrect Command

```
```
[paul@fohgnrn]$ sudo /sbin/shutdown now
Password:
Sorry, user paul is not allowed to execute "/sbin/shutdown now" as root on fohgnrn.
[paul@fohgnrn]$ 
```
```