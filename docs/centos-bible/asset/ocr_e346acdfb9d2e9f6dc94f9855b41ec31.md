A `/home/aquota` user file is created from the previous command. To create an initial `aquota.group` file, type `touch /home/aquota.group`. Next, you must create the disk usage table for the partition. Here's an example of how to do that:

```
# quotacheck -vug /home

```

The `quotacheck` command in this example looks at the file system partition mounted on `/home` and builds a table of disk usage. The `-v` option produces verbose output from the command, the `-u` option causes user quotas to be examined, and the `-g` option causes group quotas to be examined.

# ## Creating a Quota Start-Up Script

Because the quota package doesn't include a start-up script with the current CentOS distribution, you need to create your own. You want this script to check quotas (`quota` command), start the quota service (`quotaon` command), and turn off the service (`quotaoff` command).

Open a new file called `/etc/init.d/quota` as root user, using any text editor. Here is an example of the content you can add to that file:

```
#!/bin/bash

# init file for quota
#
# description: Checks disk quotas
#
# processname: quota
# chkconfig: - 90 90
# source function library
. /etc/rc.d/init.d/functions
case "$1" in
start)
    echo -n "Checking quotas: "
    daemon /sbin/quotacheck -avug
    echo -n "Starting quotas: "
    daemon /sbin/quotaon -avug
    echo
::
stop)
    echo -n "Shutting down quotas: "
    daemon /sbin/quotaoff -a
    echo
::
restart)
    $0 stop

```