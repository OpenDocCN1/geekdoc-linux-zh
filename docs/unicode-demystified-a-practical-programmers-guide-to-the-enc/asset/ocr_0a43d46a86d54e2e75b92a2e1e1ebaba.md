so that no user interfere with disk maintenance and backup programs. The classical UNIX term for this state is quiescent. See "Backing Up Files" on page 997 for a discussion of one of the most important and often neglected areas of system administration.

# Going Multiuser

After you have determined that all is well with all filesystems, you can bring the operating system up to multiuser mode. When you exit from your single-user shell, init brings you to the default runlevel—usually 3 or 5 (see Table 17-7 on page 943). Or, the following command in response to the Superuser prompt brings the system to multiuser mode:

```
# telinit 3
```

The telinit utility tells init what runlevel to enter. The telinit executable is a symbolic link to the init executable, but by convention, running telinit is preferred to running init directly.

When it goes from single-user to multiuser mode, the system executes the K (kill or stop) scripts and then the S (start) scripts in /etc/rc.d/rc3.d. For more information, refer to "rc Scripts: Start and Stop System Services" on page 944. Use onconfig (page 947) when you want to stop one of these scripts from running.

Once a machine that is connected to a network is in multiuser mode and running NFS (runlevel 3), you should be able to share local filesystems with remote machines and remote filesystems with the local machine. Add scripts that start processes as a Web server or a database to /etc/rc3.d. In general, runlevel 3 is used to provide services to other users on a network. Runlevel 2 is referred to as multiuser mode, and runlevel 3 is extended multiuser mode. Because runlevel 2 is rarely used, this chapter uses the term multiuser to refer to runlevel 3. Runlevel 4 is not used, and runlevel 5 is graphics or X11 mode.

# Multiuser Mode

Multiuser mode is the normal state for a GNU/Linux system. All appropriate filesystems are mounted, and users can log in from all connected terminals, dialin lines, and network connections. All support services and daemons are enabled and running. Once the system is in multiuser mode, you will see a login screen or prompt. Most systems are set up to boot directly to multiuser mode without stopping at single-user mode.