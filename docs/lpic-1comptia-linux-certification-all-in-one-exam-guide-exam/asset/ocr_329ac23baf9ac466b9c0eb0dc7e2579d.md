# Chapter 17: Securing Linux

![](bbox=[0.08, 0.08, 0.87, 0.35])

Figure 17-22 Using last to review login history

through a list of dictionary terms, trying them as passwords for user accounts. Like wtmp, faillog is a binary file. To view it, you need to use the faillog utility. This utility displays the user who tried to authenticate, how many times that user failed to log in, and when the last unsuccessful attempt occurred. You can use the -u option to view login attempts for a specific user account, as shown in Figure 17-23.

When reviewing this log file, look for at unusual login attempts, such as an abnormally high number of failed logins, especially if they occurred late at night. You can also use the faillog utility to specify how the system handles failed login attempts. This is done using the following options with the faillog command:

+   *   -I seconds Locks the account for the specified number of seconds after a failed login attempt
+   *   -m number Sets the maximum number of failed login attempts before the user account is disabled

The next log file is /var/log/lastlog. This file contains a list of all the users in the system and when they last logged in. As with the other log files we’ve looked at, you can’t view lastlog with less, cat, or a text editor. To view lastlog, you must use the lastlog utility from the shell prompt, as shown in Figure 17-24.

The last log file you can use to detect intrusion attempts is /var/log/messages. As mentioned earlier, this log file contains messages from all services running on the

![](bbox=[0.08, 0.93, 0.87, 0.97])

Figure 17-23 Using faillog to view failed login attempts