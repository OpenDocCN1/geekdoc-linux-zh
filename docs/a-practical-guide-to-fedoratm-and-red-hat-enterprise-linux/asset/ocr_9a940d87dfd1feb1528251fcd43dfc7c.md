to check password expiration, as a **password** module to update a password (i.e., if **login** prompts with **your password has expired, enter a new password**), or as a **session** module to record login and logout timestamps for **wtmp** (for use with the **last** utility).

# Modifying the PAM Configuration

# **Do not lock yourself out of the system**

> **caution** Editing PAM configuration files correctly requires careful attention. It is easy to lock yourself out of the system with a mistake. To avoid this problem, keep backup copies of the PAM configuration files you edit, test every change thoroughly, and make sure you can still log in after the change is installed. Keep a **root** shell open (use **su** or **sudo \-1**) until you have finished testing. If a change fails and you cannot log in, use the **root** shell to replace the newly edited files with the backup copies.

Some UNIX systems require that a user be a member of the **wheel** group to use the **su** command. Although Fedora/RHEL is not configured this way by default, PAM allows you to change this behavior by editing the /etc/pam.d/su file:

```
```
$ cat /etc/pam.d/su
...
# Uncomment the following line to implicitly trust users in the "wheel" group.
#auth		sufficient			pam_wheel.so trust use_uid
# Uncomment the following line to require a user to be in the "wheel" group.
#auth		required		pam_wheel.so use_uid
```

```

The lines of the **su** module contain comments that include the lines necessary to permit only users who are in the **wheel** group to use **su** (required) and to permit members of the **wheel** group to run **su** without supplying a password (sufficient). Uncomment one of these lines when you want the system to follow one of these rules.

# Setting Up a Server

This section discusses issues you might need to address when setting up a server: how to write configuration files; how to specify hosts and subnets; how to use **rpcbind**, **rpcinfo**, and TCP wrappers (**hosts.allow** and **hosts.deny**); and how to set up a **chroot** jail. Chapters 13 and 18−26 cover setting up specific servers; Chapter 16 discusses setting up a LAN.

# Standard Rules in Configuration Files

Most configuration files, which are typically named *\*.conf*, rely on the following conventions:

+   • Blank lines are ignored.
+   
+   • A \# anywhere on a line starts a comment that continues to the end of the line. Comments are ignored.