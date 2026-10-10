
> NOTE
> The Gentoo distribution uses named runlevels rather than numbered runlevels. This configuration can be handy if you want to define many runlevels and switch to them by name—say, for using a laptop on any of several networks.

## Temporarily Starting or Stopping a Service

SysV startup scripts reside in particular directories—normally `/etc/rc.d/init.d` or `/etc/init.d`. You may run one of these scripts, followed by an option like `start`, `stop`, or `restart`, to affect the server’s run status. (Some startup scripts support additional options, such as `status`. Type the script name without any parameters to see a list of its options.) For instance, the following command starts the Samba server on an Ubuntu 8.04 system:

```
# /etc/init.d/samba start
```

You’ll usually see some indication that the service is starting up. If the script responds with a `FAILED` message, it typically means that something about the configuration is incorrect, or the service may already be running. You should keep a few things in mind when manually starting or stopping a service in this way:

-   The name of the startup script is usually related to the package in question, but it’s not fully standardized. For instance, some Samba server packages call their startup scripts `samba`, but others use `smb`. A few startup scripts perform fairly complex operations and start several programs. For instance, many distributions include a `network` or `networking` script that initializes many network functions.
-   SysV startup scripts are designed for specific distributions and may not work if you install a package on another distribution. For instance, a Red Hat SysV startup script is unlikely to work properly on a SUSE system.
-   A startup script occasionally appears to work when in fact the service doesn’t operate correctly. You can often find clues to failure in the `/var/log/messages` file (type `tail /var/log/messages` to see the last few entries). The upcoming section “Using Log Files” covers these files in more detail.
-   One way to reinitialize a server so that it rereads its configuration files is to use the `restart` startup script command. Some server packages provide a `reload` command that makes the server reread its configuration file without shutting down, which is preferable to using `restart` if users are currently using the server. Some startup scripts don’t include a `restart` or `reload` command, though. With these, you may need to manually issue the `stop` command followed by the `start` command when you change configuration options. Some servers provide commands you can issue directly to have them reread their configuration options without explicitly restarting them as well; consult the server’s documentation for details.

Temporarily starting or stopping a service is useful when you need to adjust a configuration or when you first install a server. It’s almost always possible to reconfigure a running Linux system without rebooting it by reconfiguring and restarting its services.

## Permanently Starting or Stopping a Service

If you want to permanently change the mix of services your system runs, you may need to adjust which SysV startup scripts the computer runs. As described earlier, Linux determines which services to run by using the runlevel. In addition to the `/etc/rc.d/init.d` or `/etc/init.d` directory in which the SysV startup scripts reside, Linux systems host several directories that contain symbolic links to these scripts. These directories are typically named `/etc/rc.d/rcn.d` or `/etc/rcn.d`, where `n` is a runlevel number. For instance, `/etc/rc.d/rc3.d` is the directory associated with runlevel 3. Gentoo uses named subdirectories of `/etc/runlevels` to define its runlevels—for instance, `/etc/runlevels/default` defines the default runlevel, which the system enters when it boots.

In most distributions, the links in these directories use filenames of the form `Knn service` or `Snnservice`, where `nn` is a two-digit number and `service` is the name of a service. When the computer enters a given runlevel, it executes the `K*` and `S*` scripts in the associated directory. The system passes the `start` command to the scripts that begin with `S`, and it sends the `stop` command to the scripts that begin with `K`. Thus, the key to controlling the starting and stopping of services is in the naming of the files in these SysV script directories—if you rename a script whose name starts with `S` so that it starts with `K`, it will stop running the next time the system enters the affected runlevel.

The numbers that come after the `S` and `K` codes control the order in which various services are started and stopped. The system executes these scripts from the lowest-numbered to the highest-numbered. This factor can be quite important. For instance, you’ll normally want to start network servers like Samba or Apache after basic networking is brought up.

Gentoo is an exception to this rule. Its SysV startup script links are not named in any special way. Instead, the Gentoo startup scripts incorporate dependency information, enabling them to start the services on which they rely. This design greatly simplifies SysV administration on Gentoo systems.

Various tools exist to help you adjust what services run in various runlevels. Not all distributions include all these tools, though. The following are some of the tools for adjusting services:

-   **chkconfig** This command-line utility is most common on Red Hat and related distributions; some don’t include it. Pass it the `--list` parameter to see a summary of services and whether they’re enabled in each runlevel. You can add or delete a service in a given runlevel by using the `--level` parameter, as in **`chkconfig --level 5 smb on`**, which enables Samba in runlevel 5. (Pass it `off` rather than `on` to disable a service.)
-   **rc-update** This tool is Gentoo’s equivalent of `chkconfig`. To add a script to a runlevel, type **`rc-update add script runlevel s`**, where `script` is the name of the SysV startup script and `runlevel s` is one or more runlevel names. Replace `add` with `del` to remove a script from a runlevel. For instance, typing **`rc-update add samba default`** adds the `samba` startup script to the default runlevel, causing Samba to run when the system boots.
-   **ntsysv** This is a text-mode utility that, like `chkconfig`, is most common on Red Hat and related distributions. It presents a menu of services run at the runlevel specified with the `--level` parameter. You can enable or disable a service by moving the cursor to the runlevel and pressing the spacebar.
-   **ksysv** Figure 4.1 shows this GUI utility. It supports enabling or disabling services in any runlevel from 0 through 6. Locate and select the service in the Start or Stop section of the given runlevel, right-click the entry, and then select Cut from the pop-up menu. This removes its start or stop entry. You can then drag the service from the Available Services list to the runlevel's Start or Stop list. The system will create an entry in that runlevel and give it a sequence number based on the location at which you dropped it.
-   **Distribution-specific tools** Many distributions' general system administration tools, such as Red Hat's Service Configuration tool and SUSE's YaST, provide the means to start and stop SysV services in specific runlevels. Details vary from one distribution to another, so consult your distribution's documentation to learn more.

Once you've modified a service's SysV startup script listings, that service will run (or not run, if you've disabled it) the next time you restart the computer or change runlevels, as described in the upcoming section “Setting the Runlevel.” Setting the startup script runlevel information, however, does not immediately run or shut down a service. For that, you'll need to manually enable or disable the service, as described earlier.

### FIGURE 4.1
The ksysv program provides a GUI interface to runlevel service management.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_191_0.png)
