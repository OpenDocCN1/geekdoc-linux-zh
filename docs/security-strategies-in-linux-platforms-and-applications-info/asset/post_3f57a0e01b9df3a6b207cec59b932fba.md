
# 160 PART 2 Layered Security and Linux

> NOTE

The internet and extended internet super server services specify "internet" in lower case, as both services relate to an interconnection of networks, not to the Internet.

Some services are part of the extended internet super server. Management commands for such services are described later in this chapter.

A few services may have no scripts in the /etc/init.d/ directory or configuration files associated with the extended internet super server. In that case, you'll just have to apply the kill or killall commands to the service daemon. For example, if a hypothetical daemon is running on your system, you can run the killall command.

Alternatively, you could find the process identifier (PID) associated with the daemon and apply the kill command to PID number. The kill command is more flexible, as it can send a number of different signals to daemons that are currently running.

## Change the Service Defaults

Generally, it's fastest to change most Linux configuration options to end at the command-line interface. Two similar commands to that end are update-rc.d and chkconfig. While the commands are different, they both work with different scripts in the runlevels of 0, 1, 2, 3, 4, 5, and 6. The standard for most Linux distributions is to activate services in runlevels 2, 3, 4, and 5. In the same way, Linux distributions should be set to deactivate in runlevels 0, 1, and 6.

Major Linux distributions are converting their service runlevel system to Upstart, configured in /etc/event.d/. Once a script is converted, you'll be able to use the daemon more directly, with a command like service. As Upstart development is still in progress, details are subject to change. For more information, see http://startup.ubuntu.com/.

Wait, it seems the OCR text jumbled the update-rc.d section. Let me re-align the logical flow:

## The update-rc.d Command

If you're on an Ubuntu system, the update-rc.d command controls the configuration of service scripts in runlevels. If you want to remove a service from management—say the Samba service—run the following command:

```bash
update-rc.d samba remove
```

If you prefer to make sure the service is stopped in all runlevels, the following command deactivates the service in standard:

```bash
update-rc.d samba stop 0 2 3 4 5
```

In this case, the number specifies the priority. For example, if you see abc and def in /etc/rc.d/, the abc is stopped before def. The command doesn't work with the list of runlevels.

## Every Service Is a Potential Risk

Of course, the process can be reversed; the following command sets the service to start in runlevels 2, 3, 4, and 5:

```bash
update-rc.d samba start 2 3 4 5
```

## The chkconfig command

If you're on a Red Hat system, the chkconfig command can help. First, chkconfig --list lists all SysV-configured services and indicates they set to either off or start when the system moves to runlevel. Here is one example:

```bash
chkconfig smb 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

In this case, the Samba service is to start in runlevels 3 and 5. You can use the chkconfig command to set the service to start or stop in the runlevel of your choice. For example, the following command sets the service to start in runlevels 2, 3, 4, and 5:

```bash
chkconfig smb --level 2345
```

That command is equivalent to chkconfig smb on. You can reverse the process; with the following command deactivates Samba in runlevels 2, 3, and 4:

```bash
chkconfig smb --level 234 off
```

Alternatively, chkconfig smb off deactivates Samba in all runlevels.

## Services in Question

A minimal installation of RHEL 5 includes more services than a minimal installation of Ubuntu Server. But to set up a server for either distribution, you need to know a bit more about each service. This section examines the /etc/init.d/ directory of each distribution. On a typical installation, you'll see more services in this directory.

Table 6-2 includes active services than a minimal installation of RHEL 5 and Ubuntu Server. Look at each of these services on your systems. Most of these services appear only in one distribution. If you keep any of these services active, be sure you understand why. That knowledge can help you if a security issue arises in the future. Two services that should be retained are halt and single services. These services are associated specifically with runlevels 0 and 1, respectively.

The Action column includes the option that generally applies to most services. As you can see from the table, most of these services should be disabled on most systems. For certain services, your system may be an exception. If unsure, read the options carefully. Table 6-2 is a long list, but so is the work required to create a secure system. Once you create a secure bastion using this information, you can use it as a template for other secure systems.

### TABLE 6-2 Service scripts in Red Hat's /etc/init.d/ directory.

| SERVICE SCRIPT | DESCRIPTION | ACTION |
| :--- | :--- | :--- |
| acpid | Advanced configuration and power interface (ACPI) daemon; should remain enabled unless you don't care about power management. | Enable |
| anacron | Service that runs cron scripts if the system is down when jobs are scheduled; disable if the server is powered up 24/7. | Disable |
| apmd | Advanced power-management (APM) daemon; if ACPI is enabled, APM isn't necessary and can be disabled. | Disable |
| atd | The AT cron runs one-time jobs that are queued, and can be regulated by user as described in Chapter 7. | Maybe |
| auditd | The audit daemon is important for security-related events, including those highlighted by SELinux. | Enable |
| autofs | The automounter mounts removable and network directories on demand. | Disable |
| avahi-daemon | The Avahi daemon is the Linux implementation of the Microsoft zeroconf technology and the Apple Bonjour discovery protocol. It uses port 5353 to discover printers and shared directories on a local network. Sometimes used for sharing media via Rmbox. | Disable |
| avahi-dnsconf | For discovery of local Domain Name Service (DNS) servers. | Disable |
| bluetooth | For Bluetooth hardware support. | Disable |
| bootlog | For logging boot messages. | Enable |
| isdn | For support of ISDN modem. | Disable |
| console-setup | Initiates keyboard detection during the boot process. | Enable |
| crond | Cron daemon for regular administrative jobs. | Enable |
| cryptdisks-* | Encryption for disks. | Enable |
| cups | Common UNIX Printing System. | Disable |
| dnsmasq | For small-scale DNS and DHCP servers. | Disable |
