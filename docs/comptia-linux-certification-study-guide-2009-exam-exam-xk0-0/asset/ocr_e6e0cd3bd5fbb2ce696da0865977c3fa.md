# 298 CHAPTER 10: Securing Linux

![](bbox=[0.1, 0.12, 0.9, 0.4])

# last

The `last` command reviews the /var/log/wtmp file to show information about who has logged in (and out) since the file was created. The syntax is
`last [options] [name] [tty]`

+   - `-t YYYYMMDDHHMMSS` can be used to show who was logged in at a specific time.
+   - Providing a name will give the login information for a specific user account. The system logs in with a “pseudo user” account called **reboot** each time it gets rebooted, so `last reboot` will show a list of times the system has been rebooted since the creation of the /var/log/wtmp file.

> **Note**
> 
> Although not listed in the exam criteria, the related command `lastb` works in the exactly same way as `last`, except it searches the /var/log/btmp file and shows failed logins.

> **Note**
> 
> A few more interesting commands are `id` and `ls - f`. The `id` command has options to show information about your UID, GID, and security information. The `ls - f` command