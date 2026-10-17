
When one or more users, or all users, are specified here, the log entries that match the description will be written to all open consoles of the users specified. For example, on most systems, all messages of priority `.emerg.` or emergency, are sent to all user consoles. Most systems are configured to send shutdown and reboot messages at this priority.

## Logging active?

This is a simple yes or no question, with obvious meaning. However, what may not be obvious is that a disabled log is simply commented out in the `/etc/syslog.conf` file with a hash mark, and so the configuration details remain in the file even though it is no longer an active logging entry.

## Message Types to Log

Here the types of messages to log to the configured log destination can be specified. Any given log entry has two identifiers: its facility and its priority. The facility specifies the type of program generating the log, such as mail, daemon, cron, or locally definable facilities, named `local0` through `local7` on many Linux systems and similarly defined on other UNIX variants. The priority is the level of message on a scale of debug to emergency. The priority level used by any given program for any given message is somewhat arbitrary, as it is chosen by the author(s) of the program. However, it is safe to say that debug level messages will be incredibly verbose and unnecessary in all but the most complicated trouble-shooting situation, while emergency is reserved for messages of the utmost importance. Generally, you'll want to configure the priority of logs somewhere in the middle of this, somewhere around warning or err.

## Users and Groups

UNIX is, at its very core, a multi-user operating system. It was built from the ground up to provide services to a number of simultaneous users. Because of these features, UNIX provides a simple, but effective, method for restricting users to only the parts of the system in which they should have access. The Users and Groups module in Webmin attempts to provide a nice front end for those features of the system. Each version of UNIX has differences in how users and groups are implemented. However, Webmin hides those details quite effectively so that you never have to think about it. The Webmin Users and Groups module

edits several system files, depending on your OS. Usually, the files are `/etc/passwd` and `/etc/shadow`, for usernames and passwords, and `/etc/group` and `/etc/gshadow`, for groups and group passwords. Note that the shadow versions of the preceding files are far more secure than standard passwd files because they are only accessible by the root user. Shadow passwords are standard on most Linux distributions today, and many other systems as well.

Clicking a username or group name will take you to an Edit User page, allowing you to edit all facets of the account. Note that changing the user or group ID at some point in time after the account is created is risky, as permissions are set by ID, not username/group name. While the module will change these for you on the home directory, there may be user programs or even system programs that rely on the UID to remain the same. Also note that on some systems (Red Hat and probably other Linux distributions) the user and the user's primary group are always the same name by default. Red Hat Linux includes the `adduser` command, which will create a group of the same name and ID as the user, and therefore Webmin can do the same. You should not change this behavior, unless you really know what you're doing, as the system relies on this for much of its access control flexibility. Unlike some traditional UNIX variants, Linux users can have many secondary groups active at all times, which can be set to any group(s) you need.

## Users and Groups Module Configuration
