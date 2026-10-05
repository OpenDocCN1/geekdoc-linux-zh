# Rsh and Rcp

The name was changed to a conflict with the existing System V command rsh (restricted shell). Therefore, rather than running rshd, HP-UX runs remshd. To enable remshd on HP-UX, the following line should be present in the /etc/inetd.conf file:

```
rsh stream tcp nowait root /usr/sbin/remshd remshd
```

If there is a pound sign (#) at the beginning of this line, remove it and run the inetd-c command. Because there is no equivalent to rshd or remshd on Windows 2000, we will confine our discussion to Windows 2000 Rsh and Rcp.

Unlike UNIX systems, Rsh and Rcp do not prompt for a password if you do not specify a user name when running commands. If you issue either command, both commands assume the user name is the same as the one you are currently logged on. To avoid passwords, the remshd on HP-UX must know the user running an Rsh or Rcp command on a Windows 2000 system is "equivalent" to a user on the local system or NIS domain. HP-UX determines this user equivalency by means of two files: /etc/hosts.equiv and .rhists.

For a user to be granted access, the supplied user name must match an entry in one of these files. Also, the HP-UX system must have the user name you specified in the local /etc/passwd file or NIS map. The /etc/hosts.equiv file defines equivalency and is searched first. The .rhists files define equivalency between the HP-UX user and the Windows 2000 user resides in the HP-UX user's home directory, and is searched second. According to the manual page on hosts.equiv matches may be literal or can be obtained through the use of wildcards. For example:

+   - You can specify a particular user from any machine by placing + user_name in /etc/hosts.equiv. This won't work for the root user.
- You can specify any user from a particular machine by placing machine_name + in your hosts.equiv file. The exception to this entry is the root user.
- You can specify any user from any system by using + in your hosts.equiv file. Again, the exception is the root user.
- The root user can grant access only in in his or her .rhists file in the root's directory, with both the machine name and the user name (or plus signs) specified.

For more details, type hosts.equiv at an HP-UX command-line prompt.
We will now look at running the commands in depth. To simplify matters, I placed a "+\+" in /etc/hosts.equiv on my HP-UX system, which granted all equivalent systems and users access to run Rsh or Rcp. The user dylan was the only equivalent user name on both the Windows 2000 and HP-UX systems.