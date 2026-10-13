Linux security starts with a concept known as “discretionary access controls.” They include the permissions and ownership associated with files and directories. Default permissions on new files depend on the umask. Permissions can go further with specialized bits. Linux discretionary access controls can be configured on a more fine-grained basis with the help of access control lists (ACLs). Those ACLs support permissions given to specific users, overriding standard ownership and permissions.

Also in the realm of security is the firewall. In this chapter, you’ll examine the default firewall, how it works with the iptables command, and how it can also be configured with Red Hat firewall configuration tools. What you create can be further protected with a different kind of security known as “mandatory access control.” The RHEL 6 implementation of such is known as Security-Enhanced Linux (SELinux). Red Hat expects you to work with SELinux enabled on their exams. To that end, you’ll examine how to set enforcing modes, change file contexts, use boolean settings, and diagnose SELinux policy violations.

If you’re starting with the default installation created during the installation process, you may need to install additional packages during this chapter. If a network installation is available, take the name of the package and apply the yum install command to it. For example, to review the GUI-based firewall configuration tool, you’ll need to install it with the following command:

```
# yum install system-config-firewall
```

For more information on the process, see Chapter 7.

# INSIDE THE EXAM

# Basic File Permissions

Security in Linux starts with the permissions given to files. As everything in Linux can be defined as a file, it’s an excellent start. In any case, the related objective, once understood, is fairly straightforward:

+   - List, set, and change standard ugo/rwx permissions

Standard permissions for Linux files are defined for users, groups, and others, which leads to the ugo. Those permissions are read, write, and execute, which defines the rwx.