# “Doh! I Can’t Log In!”

Don’t worry—screwing up a setting in a PAM configuration file happens to everyone. Consider it part of learning the ropes. First thing to do: Don’t panic. As when dealing with most configuration errors under Linux, you can fix things by booting into single-user mode (see Module 8) and fixing the errant file.

If you’ve screwed up your login configuration file and need to bring it back to a sane state, here is a safe setting you can put in:

```
auth            required      /lib/security/pam_unix_auth.so
account         required      /lib/security/pam_unix_acct.so
password        required      /lib/security/pam_unix_passwd.so
session         required      /lib/security/pam_unix_session.so
```

This setting will give Linux the default behavior of simply looking into the /etc/passwd file for a password. This should be good enough to get you back in, where you can make the changes you meant to make!

# Debugging PAM

Like many other Linux services, PAM makes excellent use of the system log files. (You can read more about them in Module 8.) If things are not working the way you want them to work, begin by looking at the end of the log files and see if PAM is spelling out what happened. More than likely, it is. You should then be able to use this information to change your settings and fix your problem.

![](bbox=[0.12, 0.62, 0.25, 0.67])

If you are running in X, you can monitor the log file in real time by using the **tail** command in a window like so:

```
[root@stedford /root]# tail -f /var/log/messages
```

where * /var/log/messages* is the name of the log file that you want to monitor. If you aren’t sure which file to check, start with */var/log/messages*. Then check the */var/log* directory and see what other files are there. You can use the **tail** command with any of them. In another window, try doing what you are testing out. If PAM generates any messages, you will see them in your **tail** window immediately.

# Module Summary

This module documents the nature of users under Linux. Much of what you read here also applies to other variants of UNIX, which makes administering users in heterogeneous environments much easier with different UNIXs than NT/UNIX.

5
Manong Users