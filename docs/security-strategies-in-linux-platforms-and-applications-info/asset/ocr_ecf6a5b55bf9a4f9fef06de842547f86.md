# PART 2 | Layered Security and Linux

There are two methods to set the SUID bit on an executable file. The following command sets the SUID bit on the /home/michael/filename file:

```
# chmod u+s /home/michael/filename
```

Alternatively, the following command sets the SUID bit with read and write permissions for the user and group owners of the file:

```
# chmod 4660 /home/michael/filename
```

The SUID bit can be a security issue. A black-hat hacker may use it to access any account. While the /usr/bin/passwd command is carefully protected in a PAM configuration file, other SUID files may not be so well protected. One way to identify files on the local system with the SUID bit is with the following command:

```
# find / -perm +4000
```

One standard executable command with the SUID bit is /bin/ping. If you believe regular users should not be given access to the ping command or are paranoid about users starting a ping storm, you should unset the SUID bit on this file. To do so, run the following:

```
# chmod u-s /bin/ping
```

# The Set Group ID Bit

As described earlier in this chapter, one way for the SGID is for shared directories. In example, the SGID bit was set on the /home/special directory. Ownership of files written by user members of that project group was modified. The SGID bit makes the project group owner of all files written to the /home/special directory. One way to identify files on the local system with the SGID bit is with the following command:

```
# find / -perm +2000
```

The SGID bit is also frequently found on executable files intended to be run by groups. However, it's a way to protect certain binaries from attacks using the ptrace system call. One file protected by the SGID bit is the ssh-agent command. Without the SGID bit, a ptrace system call could bypass a passphrase-based Secure Shell (SSH) connection to a remote system.

# The Sticky Bit

Like the SGID bit, the sticky bit is also normally applied to a shared directory. It allows any user to add files and delete files from directories. Unlike the SGID bit, the sticky bit does not change the ownership of any files added to that directory. Perhaps the most common use for the sticky bit is the /tmp directory. Users who are logging into the GUI