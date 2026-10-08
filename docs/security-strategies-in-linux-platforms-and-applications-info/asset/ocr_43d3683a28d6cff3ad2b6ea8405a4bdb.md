# CHAPTER 6 Every Service Is a Potential Risk

# 159

# Uninstall When Possible

If you don't need a service, uninstall it. The process is straightforward, especially if you're familiar with the yum and apt-get commands. For example, if you want to uninstall the Samba server on RHEL 5 system, you're run the following command:

```
# yum remove samba
```

Just watch for dependencies. Before accepting what you do, watch the messages. If there are dependencies, the command will prompt for confirmation to make sure you actually want those dependent packages to be uninstalled. If there's a problem, you can always deactivate the Samba service as described in the next section.

In addition, commands that uninstall packages on Red Hat systems will often leave existing configuration files with an extension such as .rpmsave. You may want to remove such files, especially if the server has just moved to another system. Configuration could provide important clues to a black-hat hacker on weaknesses in that service.

Alternatively, to uninstall the Samba server on an Ubuntu system, you have two basic options with the apt-get command:

+   - apt-get remove samba
- apt-get purge samba

The purge option uninstalls the target package—and deletes associated configuration files. Especially because most configuration files are readable by any user, you don't want to leave any hints for black-hat hackers who break into your systems.

# Deactivate if Still in Work

If you want to keep an extra service on a system, it's best to deactivate it—in other words, turn it off, and make sure it stays off if the system has to rebooted. For example, you may be working on some special configuration for Samba. If you're not ready to put into production, that service should be deactivated. If the Samba service is not active, the associated TCP/IP ports are not shown.(Yes, if a service is inactive, there's still a risk that a black-hat hacker who gets into your system could turn on the service.)

# Stop a Service

As reboots of Linux systems are fairly rare, the first step is to directly deactivate the service. In most cases, services are controlled by a script in /etc/init.d/ directory. Depending on the distribution, script names may vary slightly. For example, the Samba server in Red Hat is smbd and samba in Ubuntu. To stop the noted script, just run it with the stop option. For RHEL, the command would be as follows:

```
# /etc/init.d/smbd stop
```

> TIP
 Ubuntu systems, some services are started in all runlevels. For a list of services, review the files in the /etc/rc.d/ directory.