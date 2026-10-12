
## Writing Your Own rc Script

In the course of keeping a Linux system running, you will, at some point, need to modify the startup or shutdown scripts. There are two roads you can take to doing this:

- If your change is to be effected at boot time only, and the change is small, you may want to simply edit the **/etc/rc.local** script. This script gets run at the very end of the boot process.

- On the other hand, if your addition is more elaborate and/or requires that the shutdown process explicitly stop, you should add a script to the **/etc/init.d** directory. This script should take the parameters **start** and **stop** and act accordingly.

Of course, the first option, editing the **/etc/rc.local** script, is the easier of the two. To make additions to this script, simply open it in your editor of choice and append the commands you want run at the end. This is good for simple one- or two-line changes.

If you do need a separate script, however, you will need to take the second option. The process of writing an **rc** script is not as difficult as it may seem. Let’s step through it using an example, to see how it works. (You can use this example as a skeleton script, by the way, changing it to add anything you need.)

Assume you want to start a special program that pops up a message every 60 minutes and reminds you that you need to take a break from the keyboard (a good idea if you don’t want to get carpal tunnel syndrome!). The script to start this program will include the following:

- A description of the script’s purpose (so you don’t forget it a year later!)
- Verification that the program really exists before trying to start it
- Acceptance of the **start** and **stop** parameters and performance of the required actions

Given these parameters, here’s the script you will write. (Notice that lines starting with a number sign (#) are only comments and not part of the script’s actions, except for the first line.)

```bash
#!/bin/sh
# 
# Carpal    Start/Stop the Carpal Notice Daemon
# 
# description: Carpald is a program which wakes up every 60 minutes and
# tells us that we need to take a break from the keyboard
# or we'll lose all functionality of our wrists and never
# be able to type again as long as we live.
#
# processname: carpal

# Source function library.
. /etc/rc.d/init.d/functions
[ -f /usr/local/sbin/carpald ] || exit 0
# See how we were called.
case "$1" in
start)
echo -n "Starting carpald: "
daemon carpald

echo
touch /var/lock/subsys/carpald
;;
stop)
echo -n "Stopping carpald services: "
killproc carpald

echo
rm -f /var/lock/subsys/carpald
;;
status)
status carpald
;;
restart | reload)
$0 stop
$0 start
;;
*)
echo "Usage: carpald start | stop | status | restart | reload"
exit 1
esac

exit 0
```

Once you have a new script written, simply add the necessary symbolic links (symlinks, as described in Module 6) from the appropriate runlevel directory to have the script either start or stop. In the sample script, you want it to start only in either runlevel 3 or runlevel 5. This is because it assumes these are the only two runlevels during which you will do normal day-to-day work. Lastly, you want the daemon to be shut down when you go to runlevel 6 (reboot). Here are the commands you enter to create the required symlinks:

```bash
[root@tedford /root]# cd /etc/rc3.d
[root@tedford rc3.d]# ln -s ../init.d/carpald S99carpald
[root@tedford rc3.d]# cd ../rc5.d
[root@tedford rc5.d]# ln -s ../init.d/carpald S99carpald
[root@tedford rc5.d]# cd ../rc6.d
[root@tedford rc6.d]# ln -s ../init.d/carpald K00carpald
```

Notice that for runlevels 3 and 5, you used the number 99 after the S prefix; this ensures that the script will be one of the last things to get started as part of the boot process. For runlevel 6, you wanted the opposite—carpals should shut down before the rest of the components. (The sequence for starting components generally goes from most critical to least critical, whereas shutting components down goes from least critical to most critical.)

Seems rather elaborate, doesn't it? Well, the good news is that because you've set up this rc script, you won't ever need to do it again. More important, the script will automatically run during startup and shutdown and be able to manage itself. The long-term benefits are well worth the overhead up front.

## Project 8-2 Creating an rc Script

This module presents an example of an **rc** script created for a repetitive stress warning message. In this project, you'll write an **rc** script for a daemon that monitors a directory and maintains an archive of its contents. For this project, assume that there exists a program, */usr/local/sbin/arch_data*, that detects changes in a specified directory and creates an archive of that directory's contents. The program is called this way: */usr/local/sbin/arch_data monitored-directory archive-directory*.

### Step by Step

1. Become **root** to edit the file */etc/init.d/arch_data* in your preferred text editor.
2. This will be a shell script, so you need to tell the system that's the case by starting the file with the string *#!/bin/sh*.
3. Add a comment explaining the purpose of this script and the program it points to. You might want to add additional helpful information, such as what arguments are passed to the program, the date you're writing it, and your name.
4. Tell the script to make use of the functions Red Hat has already provided in the */etc/init.d/functions* file by adding the string *. /etc/init.d/functions*.
5. Make sure the *arch_data* program exists; if it doesn't, exit.
6. Set the variable *MON_DIR* to the name of the directory to be monitored: *MON_DIR="~/export/research/current"*.
7. Set the variable *SAVE_DIR* to the name of the directory to hold the changes: *SAVE_DIR="~/export/research/archive"*.
8. Set up the **case** statement to read the **rc** instruction, which will be in the $1 variable.
9. If the instruction is **start**, then `echo` a message indicating that the service is starting, and run the `daemon` command on `arch_data`, passing $MON_DIR and $SAVE_DIR so the archive program knows what to do. Use the `touch` command to create the /var/lock/subsys/arch_data lock file.
10. If the instruction is **stop**, then print a message indicating that the service is stopping, and run the `killproc` command on `arch_data` program to stop it. Delete the lock file you created.
11. If the instruction is **status**, then run the **status** command on `arch_data`.
12. If the instruction is **restart** or **reload**, then stop, then start `arch_data`.
13. If the instruction is anything else, print a message listing the valid instructions and exit with an error.
14. Don't forget to close the case statement and exit without an error.
15. Add links to the new script so that it starts and shuts down properly in runlevels 2, 3, and 5.

### Project Summary

If you've never done any script programming, this may not be the world's easiest project. That's okay, but be sure to look at the example in this module to help clarify things. You can also look at the contents of the /etc/init.d directory for some more advanced examples. Each of those scripts makes use of functions defined in the /etc/init.d/functions file (including killproc, status, and daemon), and you can polish your script by following some of the examples you see there.

By storing the program's input arguments, *monitored-directory* and *archive-directory*, in variables at the beginning of the script, you make configuration changes easier. But it would be even better to create a configuration file to hold those values (for instance, /etc/arch_data.conf) so that changing the daemon's configuration wouldn't require editing the startup script.

Instead of using a background process as you did in this project, you might tackle the same problem by using a **cron** job to periodically check the contents of the directory and update the archive if there are changes. The difference would be in functionality: our mythical backup process is activated by changes in the directory, while the **cron** job would be activated at a set time. But that's food for thought: one of the beautiful aspects of Linux is the opportunity to use different tools to solve the same problem.
