If the Master Boot Record (MBR) is overwritten, the system will not boot into Linux and you need to rewrite the MBR.

# # INIT SCRIPTS: START AND STOP SYSTEM SERVICES

The first script that runs is `/etc/rc.d/rc.sysinit`, which performs basic system configuration, including setting the system clock, hostname, and keyboard mapping; setting up swap partitions; checking the filesystems for errors; and turning on quota management (page 582). This script is run by the `rc5` task (as specified by the `/etc/event.d/rc5` job definition file; see page 422 for more information).

# ## List the kernel boot messages

To save a list of kernel boot messages, run `dmesg` immediately after booting the system and logging in:

```
$ dmesg > dmesg.boot
```

This command saves the kernel messages in a file named `dmesg.boot`. This list can be educational; it can also be useful when you are having a problem with the boot process. For more information see page 553.

Next the `rcn` tasks (see “`rc2_task`” on page 422 for an example) run the `/etc/rc.d/rcn` init script, which runs the scripts for the services that need to be started when you first bring the system up and that need to be started or stopped when the system goes from single-user to multiuser mode and back down again. The init (initialization) scripts, also called `rc` (run command) scripts, are shell scripts located in the `/etc/rc.d/init.d` directory. They run via symbolic links in the `/etc/rc.d/rcnd` directories, where `n` is the runlevel the system is entering.

The `/etc/rc.d/rcnd` directories contain scripts whose names begin with the letter K (e.g., `K15httpd`, `K60nfs`, `K83bluetooth`) and scripts whose names begin with the letter `S` (e.g., `S25cups`, `S27NetworkManager`, `S55sshd`). When entering a new runlevel, each K (kill) script is executed with an argument of `stop`, and then each S (start) script is executed with an argument of `start`. Each of the K files is run in numerical order. The S files are run in a similar fashion. This arrangement allows the person who sets up these files to control which services are stopped and which are started, and in what order, whenever the system enters a given runlevel. Using scripts with `start` and `stop` arguments promotes flexibility because it allows one script to both start and kill a process, depending on the argument it is called with.

To customize system initialization, you can add shell scripts to the `/etc/rc.d/init.d` directory and place links to these files in the `/etc/rc.d/rcnd.d` directories. The following example shows several links to the `cups` script. These links are called to run the `cups` init script to start or stop the `cupsd` daemon at various runlevels:

```
$ pwd
/etc/rc.d
$ ls -1 */cups
-rwxr-xr-x. 1 root root 2947 Oct  8 04:45 init.d/cups
lrwxrwxrwx. 1 root root  14 Oct 14 20:38 rc0d/K10cups -> ../init.d/cups
```