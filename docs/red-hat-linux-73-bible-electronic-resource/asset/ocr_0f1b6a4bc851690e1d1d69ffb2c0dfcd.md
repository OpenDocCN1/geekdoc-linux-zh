# # Setting the server root directory

The ServerRoot directive specifies the directory that contains the configuration files, a link to the log file directory, and a link to the module directory. An alternative ServerRoot path name can be specified using the -d command-line argument to httpd.

```
# ServerRoot: The top of the directory tree under which the server's
# configuration, error, and log files are kept.
#
# NOTE! If you intend to place this on an NFS (or otherwise network)
# mounted filesystem then please read the LockFile documentation
# available at <URL:http://www.apache.org/docs/mod/core.html#lockfile>.
# You will save yourself a lot of trouble.
#
# Do NOT add a slash at the end of the directory path.
#
ServerRoot "/etc/httpd"
```

# # Storing the server's PID, lock, and ScoreBoard files

The Apache Web server keeps track of the PID for the running server process. It also stores information about lock files. On some systems, a ScoreBoard file is also created, to store internal server process information. You can change the locations of these files using the entries described below:

```
#

# The LockFile directive sets the path to the lockfile used when Apache
# is compiled with either USE_PCTL_SERIALIZED_ACCEPT or
# USE_FLOCK_SERIALIZED_ACCEPT. This directive should normally be left
# at its default value. The main reason for changing it is if the logs
# directory is NFS mounted, since the lockfile MUST BE STORED ON A
# LOCAL DISK. The PID of the main server process is automatically
# appended to the filename.
#
LockFile /var/run/httpd.lock

#

# PidFile: The file in which the server should record its process
# identification number when it starts.
#
PidFile /var/run/httpd.pid

#

# ScoreBoardFile: File used to store internal server process
# information. Not all architectures require this. But if yours does
# (you'll know because this file will be created when you run Apache)
# then you *must* ensure that no two invocations of Apache share the
# same scoreboard file.
ScoreBoardFile logs/apache_runtime_status
```