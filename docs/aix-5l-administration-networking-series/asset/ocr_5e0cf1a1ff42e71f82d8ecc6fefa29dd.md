# DCE INSTALLATION AND CONFIGURATION

Starting with new installations of AIX 5L, the /opt directory is now a filesystem. Administrators of AIX 4.3.3 systems may want to create this dedicated filesystem for the Linux affiliated applications available from IBM or to prepare the system for an AIX 5L migration. Please be aware that the DCE install creates a symbolic link to /usr/ppc/dce named /opt/dcellocal. Even though DCE installs to the /usr, /var, and /etc filesystems and directories, applications will expect DCELOCAL=/opt/dcellocal as set in the /etc/rc.dce start-up script.

The IBM documentation recommends making separate filesystems of 30MB each for /var/dce and /var/dce/directory (or CDS) to protect them if /var fills up. If you are running multiple DCE services on a machine, you should make /var/dce twice that size and monitor it carefully for possible expansion. You will regularly need to clean out expired credentials, logs, and audit files from this filesystem, so consider adding these housekeeping tasks to cron.

Refer to Chapter 6 for instructions on installing the AIX DCE packages that will be used on each computer in the cell. Install only the DCE packages required for the services you intend to support on each machine.

You may want to limit what network interfaces may bind to CDS and endpoint mapping by defining the RPC_UNSUPORTED_NETIFS variable. This is a valuable tool that can be extremely disruptive if incorrectly implemented. RPC will bind through all network interfaces if this variable is not set by default. To disable RPC from binding to the network interfaces en2 and en3, thus still allowing bind to en0 and en1, add the following line to the /etc/environment file before logging in to configure or start DCE:

```
RPC_UNSUPORTED_NETIFS=en2, en3
```

Now these interfaces will not RPC bind

Use the following rpcp command to display all map elements after DCE is configured:

```
# rpcp show mapping
```

Configure DCE in two steps. First configure and start the base cell services: a master security server, a cell directory server, and a time server. After these services have been configured and started, configure additional DCE services and replica servers. Use SMIT FastPath smit dce or mkdce to configure these services and register the cell name. Note that you will need to completely remove a service if a failure occurs during configuration or if you wish to make changes. You can remove a service by selecting the Unconfigure option in SMIT (Figure 24-1) or by invoking rdce. Use the lsdce command to verify the configuration status.

```
# smit dce 
# mkdce [options]
# lsdce [options]
# rdce [options]
```

+   SMIT DCE configuration (Figure 24-1)
+   Create DCE clients and servers
+   List DCE services
+   Remove DCE services