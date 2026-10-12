The -l and -a options are specified by default. The -l option specifies that each FTP session be logged via the syslog facility, and the -a option specifies that the access control configuration specified in `/etc/ftpasscess` be enabled. These two arguments are very useful and should not be removed. For other options, see the ftpd man page.

If you make any changes to `/etc/xinetd.d/vu-ftpd` or `/etc/services`, tell xinetd to reload the configuration by sending a SIGUSR1 signal, as follows:

```
kill -USR1 PID of xinetd

or

killall -USR1 xinetd
```

# ### /etc/ftpaccess

This is the main configuration file for the FTP server. This file contains configuration information in the following format:

```
keyword one or more options
```

The default `/etc/ftpaccess` file is shown in Listing 10-1.

# **Listing 10-1** *The default `/etc/ftpaccess` file*

```
class    all     real,guest,anonymous    *
email    root@localhost
loginfails    5
readme    README*    login
readme    README*    cwd=*
message    /welcome.msg    login
message    .message    cwd=*
compress    yes    all
```