
## Monitoring packet fragments

The Linux kernel controls the number of unprocessed UDP packet fragments it can handle using a high-to-low range. When unprocessed UDP packet fragment size reaches the high mark (usually 262144 bytes or 256K), the kernel throws away the incoming packet fragments. In other words, when UDP packet fragments reach the high mark, packet loss starts. The loss of packet fragments continues until the total unprocessed fragment size reaches a low threshold (usually 196608 bytes or 192K).

Because NFS protocol uses fragmented UDP packets, the above-high-to-low threshold used by Linux matters a great deal in NFS performance. You can view the current value of your high threshold size by running the `cat /proc/sys/net/ipv4/ipfrag_high_thresh` command. Similarly, you can view the low threshold value by running the `cat /proc/sys/net/ipv4/ipfrag_low_thresh` command. You can change the high values by running the `echo high_number > /proc/sys/net/ipv4/ipfrag_high_thresh`, and similarly, running the `echo low_number > /proc/sys/net/ipv4/ipfrag_low_thresh` changes the low number.

## Replicating contents among Web servers

Typically, content is developed and placed on a single (master) server and then is distributed to all the other Web servers that participate in the Web network. In this section I discuss a tool called `rdist`, which allows you to distribute contents from one Linux system to others.

### Using rdist to distribute files

The `rdist` program enables you to maintain identical copies of files over multiple hosts. It uses either the `rcmd` function calls or the remote shell (`rsh`) to access each of the target host computers.

The easiest way to get `rdist` working is to create a common account on all the machines involved and create `.rhosts` files for each target Web server system so that the common user on the name server host is allowed to run `rsh` sessions. For this purpose, create a user called `httpd` on all three systems involved. On each of the Web server systems, add a `.rhosts` file in the home directory of the `httpd` user. This file contains the host name of the `rdist` server in a single line.

The `.rhosts` file must be owned by the root user and be read-only for everyone else. This allows a user called `httpd` on the `rdist` server to run remote shell sessions on each Web server system. If you have created a back-end network as instructed in previous sections, you should use the `rdist` server’s host name associated with the back-end network interface, which enables you to keep the `rdist`-generated file traffic in the back-end network; thus, the packets will not compete with your Web traffic. The next step is to create a distfile for `rdist`. A distfile is a text file that contains instructions for `rdist` on how to perform the file distribution task. Listing 23-2 shows one such distfile, `rdist_distfile`.

#### Listing 23-2: rdist_distfile

```
# Distfile for rdist
#
# This is used to distribute files from ns.domain.com
# to www[12].domain.com systems
#
# $Author$ (kabir@ntec.com)
# $Version$
# $Date$
# $Id$

# List all the hosts that need to be updated.
# The list is created using user@hostname entries where each
# entry is separated by a whitespace character.
#
HOSTS = (httpd@www1.domain.com httpd@www2.domain.com)

# List the directories that need to be updated.
#
FILES = (//www)

# list the directories that need to be excluded from
# the update process.
EXCLUDE_DIR = (//www/cgi-data/ //www/apache //www/secured)

# Here are the commands:
# Install all directories listed in FILES for all hosts
# listed in HOSTS except for the directories that are
# listed in EXCLUDE_DIR
#
#!/FILES/ -> ${HOSTS}
install :
    except ${EXCLUDE_DIR};
```

This is really a very simple distfile. It defines a variable called HOSTS that has two entries as values: httpd@www1.domain.com and httpd@www2.domain.com. This tells rdist to use the httpd user account on both www1.domain.com and www2.domain.com for connection. The next variable, FILES, defines the files and directories for rdist to distribute. This script assumes that the staging server keeps all the files in the /www directory or partition. You can change this path or add multiple paths (separated by space).

The third variable is EXCLUDE_DIR. This variable is set to list all the files and directories that we want to exclude from getting distributed. The values that you see in the example are important. The first directory, /www/cgi-data/, is the CGI data directory to which all CGI scripts write their data. This directory will be exported to the Web server hosts via NFS, so it does not need to be copied onto each Web server via rdist. The `/www/apache` directory is where makesite writes the `/www/apache/conf/httpd.conf` file, which needs to be copied because each Web server has its very own Apache configuration file in the local `/www/apache` directory. The final value is `/www/secured`, which is used by the secured server as the document root and needs to be copied onto the Web servers. The rest of the file describes a simple command:

```shell
$ {FILES} -> ${HOSTS}
    install ;
    except ${EXCLUDE_DIR};
```

This command takes all the files and directories that the FILES variable points to and installs them on the hosts indicated by the HOSTS variable. It also tells rdist to exclude the files and directories specified by the EXCLUDE_DIR variable. To run rdist (as httpd), use the following command from the command line:

```shell
/usr/bin/rdist -p /usr/sbin/rdistd \
     -oremove,quiet \
     -f /usr/local/rdist/ rdist_distfile
```

The -p option specifies the location of the rdist program needed by rdist; the -o option specifies that one or more options are to follow—in this case, `remove` and `quiet`. The `remove` option tells rdist to remove any erroneous files found in the target system in target directories. This provides an easy method for maintaining an identical copy of the staging area on each Web server. The `quiet` option tells rdist to be as quiet as possible during the operation. The final option, -f, specifies the location of the distfile.

To reduce human error in running this command, create an sh script called `rdistribute.sh`, as shown in Listing 23-3.

#### Listing 23-3: rdistribute.sh script

```shell
#!/bin/sh
#
# This script runs rdist to update Web servers via the
# non-routable lan domain.com. The script is run
# by cron at a fixed interval.
#
# /etc/rc/rc.local starts the script to clean up
# left-over tempfiles that might have been left
# at shutdown. This process also removes the
# log file.
#
# Authors (kabor@evoknow.com)
# $Version$
# $Id$
# $Date$
# $Status

RDIST=/usr/bin/rdist
RDISTD=/usr/sbin/rdistd
DIST_FILE=/usr/local/rdist/rdist_distfile
RDIST_OPTIONS='remove,nochkgroup,nochkmode,nochkowner,quiet'
RDIST_LOCK_FILE=/tmp/rdist.lck
RDIST_LOG_FILE=/tmp/rdist.log
TOUCH_BIN=/bin/touch
DATE=`date`

# If the script is called with an argument, then
case "$1" in
    boot)
        # Because the argument is 'boot', the script is being
        # called at system start-up, so remove all old lock
        # files and logs.
        echo -n "Cleaning up distribute.sh tmp files: "
        rm -f $RDIST_LOCK_FILE
        rm -f $RDIST_LOG_FILE
        echo "complete."
        exit 0;
    ;;

    # Because the argument is 'restart,' the script
    # needs to clean up as if the system just booted.
    restart)
    $0 boot
    ;;

esac

# If the lock file exists, then don't do anything.
if [ -f $RDIST_LOCK_FILE ]; then
    exit 0
fi

# Otherwise, create the lock file using touch
$TOUCH_BIN $RDIST_LOCK_FILE

# Run rdist
$RDIST -p $RDISTD -o$RDIST_OPTIONS -f $DIST_FILE

# Remove the lock file
rm -f $RDIST_LOCK_FILE

# Write the time and date in the log file
echo $DATE >> $RDIST_LOG_FILE

# Exit the script.

exit 0
```

This script is smart enough to detect in progress the `rdistribute.sh` process by using a lock file, which can tell when a previous `rdistribute.sh` is already in progress and continuing. This can happen when a large number of files are being updated over multiple servers. The script also accepts an argument called `boot` that can be used to clean up the lock file and the log file it creates during the boot process. The script should be called from `/etc/rc.d/rc.local` as follows:

```text
/usr/local/rdistribute.sh boot
```

This script can be scheduled to run by a cron entry in `/etc/crontab`. For example, to run this script at 10-minute intervals, the following cron entry can be added in `/etc/crontab`:

```text
0,10,20,30,40,50 * * * * httpd /usr/local/rdistribute.sh > /dev/null
```

The cron daemon will run the script as `httpd`.

## Creating a RAM-based file system

You can create a temporary, small file system in RAM for high-speed access. The reason this is a small file system is because, by default, the maximum amount of RAM that ramfs can use is one-half of the total RAM on your system. So, if you have 2GB of RAM, ramfs can only use 1GB. Because I haven't yet seen systems with more than 4GB of RAM, even 2GB ramfs is really small compared to today's large drive-based file systems. The ramfs is perfect for many small files that need to be accessed fast. For example, I use ramfs for a set of small images used in a heavily accessed Web site.

### Enabling a RAM-based file system

To use ramfs, you must enable ramfs support in the kernel as follows:

- 1. Get the latest Linux kernel source from www.kernel.org and extract it into `/usr/src/linux-version` directory as root, where `version` is the current version of the kernel. For this material, I assume that this is 2.4.1.
- 2. Select the File systems submenu. By using the spacebar, select Simple RAM-based file system support to be included as a kernel module and exit the submenu.
- 3. Ensure that all other kernel features that you use are also selected as usual.
- 4. Exit the main menu and save the kernel configuration.
- 5. Run the `make dep` command as suggested by the `menuconfig` program.
- 6. Now run `make bzimage` to create the new kernel. Then run `make modules` and `make modules_install` to install the new modules in appropriate location.
