# A user and a group for the standalone server

Like the Port directive, the User and Group directives in the httpd.conf file are meaningful only for a standalone server. The syntax for these directives is as follows:

```
User [username | #UID]
Group [group name | #GID]
```

These two directives are very important for security reasons. When the primary Web server process launches a child server process to fulfill a request, it changes the child's UID and GID according to the values set for these directives.

If the child processes are run as root user processes, a potential security hole is opened for attack by hackers. Allowing the capability to interact with a root user process maximizes the risk of a potential breach of security in the system; hence, this user capability is discouraged. Rather, choose to run the child server processes as very low-privileged users belonging to a very low-privileged group. The user named nobody (usually UID = -1) and the group named nogroup (usually GID = -1) are low-privileged. Consult your /etc/group and /etc/passwd files to determine these settings.

If you plan to run the primary Web server as a nonroot (regular) user, it will not be able to change the UIDs and GIDs of child processes, because only root user processes can change the UIDs or GIDs of other processes. Therefore, if you run your primary server as the user named foobar, all child processes will have the same privileges of foobar. Similarly, whatever GID you have also will be the GID for the child processes.

If you plan to use the numeric format for UIDs and/or GIDs, you need to insert a # symbol before the numeric value, which can be found in the /etc/passwd and /etc/group files.

# Configuring common directives

The standalone and inetd-based servers share the following common directives:

```
CustomLog path/to/logfile
```