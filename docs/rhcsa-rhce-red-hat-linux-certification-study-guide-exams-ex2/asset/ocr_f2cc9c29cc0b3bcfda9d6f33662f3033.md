# Basic Firewall Control

8. The TCP/IP port number associated with the FTP service is 21.

9. The full path to the file with RHEL 6 firewall configuration rules is /etc/sysconfig/iptables.

# A Security-Enhanced Linux Primer

10. The command that configures SELinux in enforcing mode is:

```
# setenforce enforcing
```

11. The command that lists the SELinux status of current users is:

```
# semanage login -l
```

12. The directory includes boolean settings for SELinux is:

```
/selinux/booleans
```

# LAB ANSWERS

# Lab 1

In some ways, Lab 1 could have been split into two different labs. It's designed to let you practice configuring those permissions required to set up executable scripts for user owners and other users. Success with the script is straightforward; if it's executed, you'll find a file named filelist, with a list of files, in the local directory.

It's also designed to help you understand the effect of the SUID bit of /usr/bin/passwd, a compiled executable.

# Lab 2

Lab 2 is essentially an extension of Lab 1, in that ACLs are another approach to making a script, owned by the root administrative user, executable by a single regular user. You can check for success in the same way; if the script is properly executed by the ACL configured regular user, you'll find a file named filelist in the local directory.

# Lab 3

The configuration of ACLs on the /root administrative directory is a bad security practice. However, it is an excellent way to illustrate the capabilities of ACLs on a system, how it can allow access by