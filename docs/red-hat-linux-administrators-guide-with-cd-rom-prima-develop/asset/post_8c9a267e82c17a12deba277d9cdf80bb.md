
equivalent to issuing a “shutdown” command while the latter is equal to a “reboot”.

## Running Program Specific Scripts

Sometimes you will want to install programs that will need to boot up automatically in case of a reboot or power failure. You might not always have access to the machine when it first comes back up, so you want to make sure that your program starts up by itself. In cases like these where there is no RPM or binary version of the program and you are compiling the executable from source, you will need to create a customized script.

If you lack a broad understanding of how to create a bootup script, you can usually copy an existing script and then modify it for your own use. This, however, is not a foolproof method, especially if you lack experience in programming languages. Another way is to create a very simple script that accomplishes the same means of starting up but without all the extraneous options or commands typical of other scripts.

For an example this time, let’s use the Apache Web server. You can install the RPM version of Apache on most any Linux box running Red Hat, which in turn installs all the startup scripts. However, you might want to compile the source code yourself to optimize some of the more advanced modules or simply to try your hand at compiling source. There are advantages to both methods, which won’t be examined here, but both also have their disadvantages. For more information on compiling programs from source, see Chapter 11, “Installing Additional Programs.” This chapter also discusses the difference between using both source and binary programs under Linux.

After successfully compiling and executing the program you will want confirm that should the machine lose power and need to be rebooted or if for some other reason it needs assistance in restarting, the web daemon will restart as well.

Here is a sample script that you can place in the `/etc/rc.d/rc3.d/` directory. It is called S99apache. The initial character needs to be capitalized so that the bootup will recognize it. If you want to disable this function yet keep the script, merely change the capital S to a lowercase s. The letter S signifies starts, while the other initial letter, K, denotes kill and is used to shut down certain daemons. Listing 2.5 shows how this simple script starts the web daemon.

### Listing 2.5 A Sample Script for Starting a Release of Apache that Was Compiled from Source

```bash
# Start http daemon - Apache
#
if [ ! -f /usr/local/etc/httpd/src/httpd ]; then
    /usr/local/etc/httpd/src/httpd -f /usr/local/etc/httpd/conf/httpd.conf;
    echo "Starting Apache"
fi
```

This script simply checks for the Apache binary located in /usr/local/etc/httpd/src/. If the binary file is present, the program starts the daemon with the appropriate configuration file. It also prints out a simple statement informing the user that the web daemon is starting.

Apache is a fairly standard program and is used by most Linux boxes. However, if you want to use other less familiar programs, such as Big Brother, a network monitoring program that informs administrators of the status of all machines on the network, you would use a customized script.

Listing 2.6 shows a sample script, named bb, that you would include in a file that you would first create in the /etc/rc.d/init.d/ directory. You would need to change the permissions to make this script executable. Also, Big Brother requires that the bb user, here referred to as abuser, be the only user able to execute the script. It is yet another security hole if you allow root to execute this script. Notice on the last line how root changes to the user, abuser, to then execute the script.

### Listing 2.6 A Sample Script that Executes the Big Brother Daemon, which Monitors Machines on a Network

```bash
#
# Start the BigBrother daemon
#
if [ -x /usr/local/gnu/bb/runbb.sh ]
then
    #
    # Make sure BB is shut down
    #
    sh /usr/local/gnu/bb/runbb.sh stop > /dev/null 2>&1
```

## STARTING UP AND SHUTTING DOWN

```bash
#
# Initialize a new logfile
#
> /usr/local/gnu/bb/BROUT

echo "Starting up Big Brother ..."
su - buser /usr/local/gnu/bb/runbb.sh start

fi
# EOF
```

After creating the main file, you would copy the same scripts created by the default Red Hat Linux install and place symbolic links in each of the different run states. For example, in the /etc/rc.d/rc3.d/ and /etc/rc.d/rc5.d/ directories, you would place a link pointing back to the original script and name the new file S99bb. You create this file by typing the following:

```bash
[root@pluto init.d]# cd /etc/rc.d/rc3.d/
[root@pluto rc3.d]# ln -s ../init.d/bb S99bb
[root@pluto rc3.d]# ls -la S99bb
lrwxrwxrwx 1 root  root   1  May  3 12:07 S99bb -> ../init.d/bb
```

You can do the same for nearly any script. If the run level is not important, then another location to place startup scripts is the /etc/rc.d/rc.local or /etc/rc.d/rc.sysinit file. These files can be optimal locations for various utilities such as one that sets the hardware clock to another time clock. The following is an example script that you could place in the /etc/rc.d/rc.local file. This file simply updates the system clock by executing the ntpdate command and logging into a server that has the correct time.

```bash
# Update the time upon bootstrap
/usr/sbin/ntpdate -b 129.237.32.1
```

It is up to the administrator to determine what needs to be started upon bootup. Only by testing the various scripts and modes in different directories will you be able to see what formats works best for you.

## Changing the State of Linux Operations

Linux operates on many levels. While a client is logged in, working on certain tasks, the system itself might also be running various routines and programs.

Changing the state of the system without saving information to the disk can be disastrous, both for the operating system and for your own files. A Linux administrator should be familiar with the methods of properly bringing a system down so that it is safe to power off. An administrator should also know how to change the system’s current *run level*, or state of performance, whether it is in single- or multiuser mode, before executing anything that might alter the status quo.

This section will look at some methods to shut down Linux properly without damaging file systems as well as to change its run level state so that administrative tasks can be carried out.

### Shutting Down

It is unwise simply to press the power button on a Linux box when you want to shut down the system. This can result in the corruption of files and loss of data. Constant mismanagement of the system and repeated shutdowns in this manner over time can cause serious damage to the software, both the operating system and any programs you may have installed. Linux constantly accesses files while in all run level modes (except for that of run level 0) and keeps the hardware in a ready state of alert. Cutting power to the system renders files unable to write back to the disk and can physically damage the hardware. Linux is not like MS-DOS or other non-multitasking operating systems, which encourage the user to shut down the machine once it has returned to a command-line prompt. MS-DOS is the only one on which the user can suddenly kill the power with assurance that all the files will remain safe. Every other operating system, from Windows 9x to NT to Novell NetWare to all flavors of UNIX, must be shut down in an orderly and safe manner. In the case of Linux, special commands must be given to bring the system down to a safe state so that power can be turned off. Also, only root has this privilege, to prevent any other user from shutting down the machine.

> **NOTE**
>
> This is no longer true with the latest Red Hat Linux release. A regular user can shut down a Linux box after logging into the GUI. The GNOME environment, for example, provides the option to halt or shut down the system after logging out. The only stipulation is that you provide the password of the user currently logged in.
