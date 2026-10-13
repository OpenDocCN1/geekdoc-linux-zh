New password:
Retype new password:
passwd: all authentication tokens updated successfully
(Warned testdud e, now sleeping 10 seconds)
testdud e was logged in. Just logged testdud e out.
Account testdud e has been suspended.

The user testdud e would have seen the following pop up on his screen:
**************************************************
URGENT NOTICE FROM THE ADMINISTRATOR:

This account is being suspended by the request of management.
You are going to be logged out in 10 seconds. Please shut down
any processes you have running immediately.

If you have any questions, please contact your supervisor or
Jane Mansmith, director of information technology.
**************************************************

And, sure enough, ten seconds later testdud e would be logged out and unable to log back in.

![](bbox=[0.22, 0.6, 0.3, 0.7])

Compatibility-wise, the third field of the ps output on BSD systems is the parent process ID (PPID) rather than the session ID. The good news is that it'll work just as well for this task, so the script works across platforms, with but one small change necessary: homedir must be defined as appropriate for each server.

+   4. To re-enable an account after you've suspended it is sufficiently straightforward enough that I'll just show you the snippet of the shell script (unsuspend) that does the work:

```
passwd $1   # change their password back to a known value
chmod 750 $homedir/$1  # and open their home directory back up
```

There are other ways to suspend accounts on some Unix systems that are worth mentioning. If you're running Linux, for example, there's usermod, which lets root change the status of a user account. With the -L flag, it locks the account, disabling the password by prefixing the encrypted password string with a !, and with -U it removes that ! and enables the account again.

Solaris uses the passwd command to enable suspension: passwd -l acct will lock the specified account (specifying a new password with the standard passwd acct will unlock the account again).