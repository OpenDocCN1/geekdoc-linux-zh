option displays the OS name (for instance, Linux). The -v option displays the local build version of the OS (for instance, #1 Tue Oct 13 22:17:11 EDT 1998).

# uptime

Syntax:

```
uptime
```

The uptime command displays the current time; how long the system has been up since the last reboot; how many users are connected to the server; and the system load in the last 1, 5, and 15 minutes.

# User Administration Commands

The commands in this section pertain to user administration.

# chfn

Run the chfn command to change a user's finger information. For example, the following enables you to change user jennifer's finger information, which is stored in the /etc/passwd file:

```
chfn jennifer
```

A user can change his or her own finger information by using this program, as well. A user can also create a .plan file in his or her home directory that will get appended to the information shown by the finger program.

# chsh

Use the chsh command to change a user's shell. For example, the following enables you to change user brian's current shell:

```
chsh brian
```

If you specify any shell or program name that is not in /etc/shells, the user will not be able to log in. Note that a user can change his or her own shell using this command. An ordinary user does not need to specify the