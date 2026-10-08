# 1496

# uucp, uulog, uaname

uulog
The following options print logging information.

+   - ssys Print information about file transfer work involving system sys
- fsystem Do a tail -f of the file transfer log for system (You must press the Break key to exit this function.)

Other options you can use in conjunction with the above options are:

+   - x Look in the uuuxqt log file for the given system.
- number Execute a tail command of number lines.

# uaname

+   - c Display the names of systems known to cu. The two lists are the same unless your system is using different Systems files for cu and uucp. See the Sysfiles file.
- 1 Display the local system name.

# Operands

The source file may be a path name on your system or may have the form: system-name!pathname
source-file is taken from a list of system names that uucp knows about. source-file is restricted to no more than one system-name. The destination system-name can also include a list of system names such as system-name!system-name!...system-name!pathname

With this syntax, uucp tries to send the file to the destination, using the specified route. Take care to ensure that intermediate nodes in the route are willing to forward information.

> Note The forwarding of files through other systems may not be compatible with the previous version of uucp. If you use forwarding, all systems in the route must have compatible versions of uucp.

For C shell, surround the ! character with single quotes (''), or precede it with a backslash(\).
The shell metacharacters ?, and [...] appearing in pathname are expanded on the appropriate system.
Paths can be one of the following:

+   - An absolute path name.
- A path named by -user where user is a login name on the specified system and is replaced by that user's login directory.
- A path named by -destination where destination is appended to /var/spool/uucpublic.

> Note This destination is treated as a file name unless you are transferring than one file with this request or the destination is already a directory. To ensure that the destination is a directory, follow it with a slash (/). For example ~/dan/ as the destination creates the