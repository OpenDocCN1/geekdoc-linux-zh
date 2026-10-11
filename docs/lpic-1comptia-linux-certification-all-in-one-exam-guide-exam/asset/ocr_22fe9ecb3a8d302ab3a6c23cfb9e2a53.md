Recall in the preceding chapter that I mentioned that one of the first things I do after installing a new Linux system is to go through and turn off all of the unneeded services that run automatically. This saves memory and CPU utilization and also plugs security holes in the system. In this part of the chapter, we’re going to discuss how this is done. We’ll cover the following topics:

+   * About init scripts
+   * Configuring the default system runlevel
+   * Changing runlevels from the shell prompt
+   * Configuring services to run by default at a specified runlevel

Let’s begin by learning about init scripts.

# About init Scripts

The system processes on your Linux system are started and stopped using an *init* script. An init script is used by the init process to start processes on system boot and whenever the current runlevel is changed. These scripts are stored in a specific directory on your Linux system. Which directory they are stored in depends on your Linux distribution. Most Linux distributions use one of two types of init scripts:

+   * **System V** Linux distributions that use System V init scripts store them in the /etc/rc.d directory. Within /etc/rc.d are a series of subdirectories named rc0.d through rc6.d. Each of these directories is associated with a particular runlevel. Within each of these subdirectories are symbolic links that point to the init scripts for your system daemons, which reside in /etc/rc.d/init.d. Red Hat Linux and Fedora use System V–type init scripts.
+   
+   * **BSD** Linux distributions that use BSD-style init scripts store them in the /etc/init.d directory. Within /etc/init.d are a series of directories named rc0.d through rc6.d. As with System V init scripts, these directories are associated with a specific runlevel. These directories contain links that point to the init scripts in /etc/init.d. SUSE Linux uses this type of init script.

In addition to using the init process to run these scripts, you can run these scripts from the command prompt. Simply enter /etc/init.d/*script_name* at the shell prompt (on a BSD-style system) or /etc/rc.d/init.d/*script_name* (on a System V–style system). If you’re not sure of which script name you should use, you can use the ls command to generate a listing of scripts in the init script directory, as shown here:

```
```bash
f62:/etc/init.d # ls
...
aacpvntd          boot.lvm              lm_sensors           rpmconflycheck
acpid             boot.md               mcelog               rcined
aliasd            boot.multiptah        mdadm                setterial
ard               boot.proc             multipathd           single
audtd             boot.rootfack         network              skelelon
autofs            boot.startpreload     network-remotefs     skelton.compat
autoyast          boot.swap              nfs                 smarthd
avahi-daemon      boot.sysctl           nmb                  smb
```
```