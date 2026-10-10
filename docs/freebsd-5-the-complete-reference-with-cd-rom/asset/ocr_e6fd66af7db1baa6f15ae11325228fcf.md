and using intrusion-detection tools such as Tripwire. If you do detect an intrusion, knowing how to handle it can be very important.

# General Warning Signs

Fortunately, most crackers aren't very skilled. Script kiddies commonly invade poorly secured computers, and the root kits they use frequently leave traces behind. These traces may include modified utilities that don't work quite like the originals, modified configuration files that damage normal functionality, and so on. You should be on the lookout for certain warning signs that sometimes indicate an intrusion:

+   - **Broken programs** If a program suddenly stops working, investigate the matter. For instance, if a common program such as `ls` or `cat` suddenly starts crashing, it could be that the program has been replaced with one written or modified by a cracker.

+   - **Odd program behavior** Less serious problems than out-and-out crashes may signal an intrusion. In the UNIX world generally, programs such as `ifconfig`, `grep`, and `netstat` work differently on different platforms. Even in FreeBSD alone, these programs also change over time; options in FreeBSD 5.0 may be slightly different than those in FreeBSD 4.6, for instance. A cracker might have replaced one of these tools with a modified version derived from a non-FreeBSD source or from an earlier or later version of FreeBSD than you're using. If so, the program's output or options may suddenly change, from your point of view.

+   - **Changes in resource use** Sometimes crackers break in to steal your CPU time, network bandwidth, or other resources. Chapter 28 describes how to monitor many of these resources. If you notice a sudden change in these factors, you should investigate the cause to be sure it's not malicious activity.

+   - **Forgotten passwords** If a user comes to you and claims to have forgotten a password, investigate further. Ask the user when the account was last used, then check `/var/log/auth.log` to see if there were any logins after that date. If there were, it could be the password hasn't been forgotten, but has been changed by a cracker.

+   - **Suspicious account activity** You may notice that a user is logged in at a peculiar time (say, as listed in the output of `ps` or `who`). For instance, if you know a particular person is on vacation with no network access, but you see that user logged in using a local terminal, it could be that a cracker has broken into the user's account.

+   - **Gaps in log files** Crackers sometimes delete lines from log files, or even entire log files, to mask their activity. If you notice such gaps, you may want to investigate further. For instance, you can use the `find` command (described in Chapter 8) to locate files that were created or modified within the gap period. Be very suspicious if any critical system binaries or configuration files were modified at that time.