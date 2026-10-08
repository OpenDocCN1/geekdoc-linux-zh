# Passwords—A Key Point for Good Security

A stale account's password will not be changed, thereby leaving a hole. If they have data that needs to be reassigned, disable their account by putting a "*" or "!" in the user's password field in the /etc/passwd file. This disables logging in via that account because no password encrypts each of these values and shadow password-code understands these sequences. Gets cleaned up as soon as possible. Make sure that no set-UID or set-GID programs or publicly readable or writable files containing confidential data remain owned by that account.

Issuing

```
chmod 0 /home/someone
find /user someone -ls
```

It is a good start. Note that the user may have a mailbox, entries on mailing lists, files in the print spool directory, accounts in various applications, etc. that will need to be attended.

Note that some of the services you removed (while correcting an earlier sin) accounts in the /etc/passwd file. When you remove that service, make sure that the /etc/passwd account is also removed or disabled. Some of the notables are FTP, NFS, uucp, mail, gopher, and news. If you do not need them, get rid of them.



In many reports of intrusions the SysAdmin says, "I meant to install...TCP Wrappers...a newer version of a...firewall...meant to turn off NFS... Clearly knew, at least vaguely, what had to be done until it was too late. Sure, you have more responsibilities than time, but consider aside an hour twice a week to upgrade security.

This book is organized so that it may be used as a workbook, with the most urgent and fundamental problems discussed first. This allows you to pop a book marker in it and advance the marker every few days.

# 2.3 Passwords—A Key Point for Good Security

![](bbox=[0.215, 0.693, 0.605, 0.738])

Good passwords and good password policy are absolutely critical to security on any computer. Some of this will be familiar to experienced SysAdmins, but everyone gets busy at times, so this is a good time to review these issues and make the necessary changes. Even the author's systems were in need of a password "tune-up." It is suggested that you advise your users not to let know their passwords or see type passwords in. Explain that they should not tell a significant other, boss, or even what password is being used.

Ask each of them to report to you if anyone tries to obtain a password or if someone might have obtained one. Explain that your interest is only in security and that user's name in any of his reports of problems will be kept confidential.