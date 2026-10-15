# pwd—displays the present working directory name

# quota—displays users' disk usage and limits

```
quota [ -guvv | q ]
quota [ -uvv | q ] user
quota [ -guv | q ] group
```

quota displays users' disk usage and limits. By default, only the user quotas are printed.

+   -g Prints group quotas for the group of which the user is a member.
+   -u An optional flag, equivalent to the default.
+   -v Displays quotas on file systems where no storage is allocated.
+   -q Prints a more terse message, containing only information on filesystems where usage is over quota.

# rcp—remote file copy

```
rcp [ -p ] filename1 filename2
rcp [ -pr ] filename...directory
```

The rcp command copies files between machines in the following form:

```
remotehostname:path
user@hostname:file
user@hostname.domainname:file
```

# EXAMPLE A.43

+   1 rcp dolphin:filename /tmp/newfilename
+   2 rcp filename broncos:newfilename

# EXPLANATION

+   1 Copies filename from remote machine dolphin to /tmp/newfilename on this machine.
+   2 Copies filename from this machine to remote machine broncos and names it newfilename.

# rdate—gets the date and time via the network

```
rdate [-p] [-s] [host...]
```

rdate uses TCP to retrieve the current time of another machine using the protocol described in RFC 868. With the -p option, rdate prints the time retrieved from the remote machines. This is the default mode. With the -s option, rdate sets the local system time from the time retrieved from the remote machine. Only the superuser can reset the time. The time for each system is returned in ctime(3) format.