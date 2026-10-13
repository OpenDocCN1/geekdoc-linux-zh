+   - `-d` — Is an alias for `atrm`.
+   - `-v` — For `atq`, shows completed but not yet deleted jobs in the queue; otherwise shows the time the job will be executed. Times displayed will be in the format “1997-02-20 14:50” unless the environment variable `POSIXLY_CORRECT` is set; then, it will be “Thu Feb 20 14:50:00 1996”.
+   - `-c` — Cats the jobs listed on the command line to standard output.

# FILES

+   - `/var/spool/at`
+   - `/var/spool/at/spool`
+   - `/proc/loadavg`
+   - `/var/run/utmp`
+   - `/etc/at.allow`
+   - `/etc/at.deny`

# SEE ALSO

`cron(1), nice(1), sh(1), umask(2), atd(8)`

# BUGS

The correct operation of batch for Linux depends on the presence of a proc type directory mounted on `/proc`.

If the file `/var/run/utmp` is not available or corrupted, or if the user is not logged on at the time at is invoked, the mail is sent to the userid found in the environment variable `LOGNAME`. If that is undefined or empty, the current userid is assumed.

at and batch as presently implemented are not suitable when users are competing for resources. If this is the case for your site, you might want to consider another batch system, such as nqs.

# AUTHOR

at was written mostly by Thomas Koenig, `ig25@rz.uni-karlsruhe.de`.

# CAT

# NAME

`cat` — Concatenate files and print on the standard output.

# SYNOPSIS

```
cat [OPTION] [FILE]...
```