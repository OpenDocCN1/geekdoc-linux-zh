```
Do you want to edit the configuration file? (y/n) [n]: n
```

The Tru64 UNIX kernel is then built based on the kernel configuration options selected.

As of this writing, IP Version 6 is not supported on TruCluster Server so please do not select IP Version 6 when you do your own Tru64 UNIX kernel configuration. At a minimum, please review the TruCluster Server Release notes on what is and is not supported when it comes to kernel configuration options.

```
The system will now automatically build a kernel
with the selected options and then reboot. This can take
up to 15 minutes, depending on the processor type.

When the login prompt appears after the system
has rebooted, use 'root' as the login name and
the SUPERUSER password that was entered during
this procedure, to log into the system.

*** PERFORMING KERNEL BUILD ***
    Working..... Tue Jan 22 20:35:41 PST 2002

The new version ID has been successfully set on this system.
The entire set of new functionality has been enabled.

This message is contained in the file /var/adm/smlogs/it.log for
future reference.
```

At this point, the system will reboot. As soon as the system restarts, it will run on the newly built Tru64 UNIX kernel.

# 5.5    Configuration of *Tru64 UNIX*

In the previous section, we discussed what it takes to do an actual installation of Tru64 UNIX. In this section, we will continue with our example and do a quick configuration of Tru64 UNIX. Remember that our ultimate goal in presenting this example is to perform a successful deployment of TruCluster Server.

As you can see, the installation of Tru64 UNIX in the previous section went quite smoothly. Now that the installation is complete, the actual configuration of Tru64 UNIX takes place.