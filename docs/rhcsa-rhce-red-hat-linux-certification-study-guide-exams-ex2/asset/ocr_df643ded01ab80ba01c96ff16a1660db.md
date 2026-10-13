user on each line, as in files like /etc/cron.allow, or it could be in a list that follows a directive, such as

```
valid users = michael donna @book
```

Sometimes the syntax of a user list is unforgiving; in some cases, an extra space after a comma or at the end of a line may result in an authentication failure.

Groups are frequently included in a list of users, with a special symbol in front, such as an @ or an +.

Sometimes, users who are allowed access to a system are configured in a separate authentication database, such as that associated with the Samba server, configured with the smbpasswd command.

# Console Security

As discussed in Chapter 8, console security is regulated in the /etc/securetty and /etc/security/access.conf files. It can help you regulate local console access to root and regular users.

But console access is not just local. For a full view of console security, you need to be able to configure limits on remote console access. Two primary options are SSH as discussed earlier, and Telnet. While the telnet command has its uses, as described in Chapter 2, communications to Telnet servers are inherently insecure. User names, passwords, and other communication to and from a Telnet server are transmitted in clear text. That means a network protocol analyzer such as Ethereal could be used to read those user names, passwords, and any other critical information.

Even though Kerberos-based options are available for Telnet servers, most security professionals avoid Telnet for remote consoles at almost all costs. And that's consistent with the recommendations from the NSA.

# Recommendations from the U.S. National Security Agency

The NSA has taken a special interest in Linux, and specifically Red Hat Enterprise Linux. Not only has the NSA taken the time to develop SELinux, but also it has created guides to help administrators like yourself create a more secure RHEL configuration. (Yes, the "super-secret" NSA has released SELinux code under open-source licenses for all to see.) They recognize the importance of Linux in the infrastructure of computer networks. Observers of RHEL may notice how changes between RHEL 5 and RHEL 6 follow NSA recommendations.