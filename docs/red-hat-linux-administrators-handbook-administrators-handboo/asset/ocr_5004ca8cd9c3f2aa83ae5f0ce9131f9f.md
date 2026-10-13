# The /etc/rc.d/rc.sysinit script

As you already know, when a Red Hat Linux system boots, the kernel runs init, which in turn runs the /etc/rc.d/rc.sysinit script before processing any other scripts for the desired run level. The following line in the /etc/inittab file causes init to run this script before running anything else:

```
si::sysinit:/etc/rc.d/rc.sysinit
```

Notice that the run level field is empty, because init recognizes sysinit as a system initialization action. The rc.sysinit script does many things, including setting the host name, enabling the swap partition, checking the file systems, loading kernel modules, and more. Typically, you do not need to modify this script.

# The /etc/rc.d/init.d directory

The init.d subdirectory is used to store all the scripts needed for all the run levels. Keeping all the scripts in one location makes managing them easier. Each script is used to start/stop a particular service—Domain Name Service (DNS), Web service, or another such service. All of these scripts follow a special command-line argument syntax. For example, to start NFS (Network File System) service, you can run the following script:

```
/etc/rc.d/init.d/nfs start
```

To stop the same service, you can run the same script as follows:

```
/etc/rc.d/init.d/nfs stop
```

The nfs script takes start and stop as arguments. This is true for all the scripts in this directory, which are symbolically linked to the rc0.d through rc6.d directories, as needed.

# The /etc/rc.d/rc script

When init is told to change the run level to one of the seven possible run levels, it runs a script specified in one of the following lines in the /etc/ inittab file:

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
```