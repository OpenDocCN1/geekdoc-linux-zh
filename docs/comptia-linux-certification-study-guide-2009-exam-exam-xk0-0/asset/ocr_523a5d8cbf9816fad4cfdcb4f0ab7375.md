# NIS

Network Information System \[NIS\] is another option for storing centralized user and other configuration files. It was originally called the "yellow pages," so many NIS commands and files start with “yp.”

NIS is comprised of one or more servers that contain a database of configuration files that are to be shared across the network and clients that are configured to access them. By sharing /etc/passwd, /etc/group, and /etc/shadow files, a user's login account information will work on any client in the system.¹²

# RADIUS

Remote Authentication Dial In User Service \[RADIUS\], as the name indicates, was originally developed for dial-in access via modems. The RADIUS client software runs on the device to which the user is attempting to authenticate. The client forwards the user information to a RADIUS server, which grants or denies the request for access. The actual password is never sent over the link.¹³

# Two-Factor Authentication

Two-factor authentication refers to a requirement to provide two things when you log in. These are usually “something you know” – a memorized password – and “something you have” – an access token of some sort. Two-factor authentication makes it much harder to break into someone else's account because just guessing their password is no longer good enough.

# SUMMARY OF EXAM OBJECTIVES

While “security” is frequently associated with “restrictions,” it’s helpful to consider it in terms of “allowances.” To summarize, remember that the `adduser` command creates accounts to allow access to the system, `chmod` modifies what users can do with files, and `groupadd` allows users to share information amongst themselves. The `su` and `sudo` commands extend user privileges to allow administrative tasks, and `ssh` and `vnc` allow users access to other systems. User account information can be shared between systems with `ldap` or `nis`, and authentication requirements can be customized using on a Linux system with `pam`.

There are number of applications for observing the Linux system environment, including

+   - Nessus and nmap for scanning networks.
+   - Wireshark for capturing packets on a network interface.