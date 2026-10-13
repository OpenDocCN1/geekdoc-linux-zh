
## FIGURE I-16

Boot devices in the Virtual Machine Manager.

![](img/9139201cfcaf4292284a0eed074928e5_45_0.png)

- 3. If the default boot device is set to CDROM, you should be able to change it to Hard Disk (or vice versa) using the arrow buttons. Once your selections are complete, click Apply. Be aware, the changes aren't implemented until the next time the KVM VM is powered on.
- 4. Click View | Console. If you haven't already done so, click Reboot to complete the RHEL 6 installation process.
- 5. Click Virtual Machine | Shut Down | Force Off. Confirm if prompted.
- 6. Click Virtual Machine | Run. The system should then boot normally into the newly installed system.

> *As of this writing, the Virtual Machine | Shut Down | Reboot and Virtual Machine | Shut Down | Shut Down menu options do not work.*

In most installations, RHEL 6 will start the first boot process discussed later in this chapter.

# CERTIFICATION OBJECTIVE I.06

# System Setup Options

Baseline configurations are important. Once configured, you can clone that baseline to set up as many systems as needed. On a real network, a good baseline can be used to create systems dedicated to specific services. To enable remote access, it will have a Secure Shell (SSH) server, configured with a regular user.

For the boot process, RHEL 6 includes an implementation of the Upstart system, which replaces the Unix-based SysVinit system. It determines the consoles, services, and displays, as well as the runlevel that starts when a system is booted. Some systems use remote authentication, configured to connect to remote servers for username and password verification. While these systems are covered in other chapters, enough information is provided in this section to set up a baseline system.

# The First Boot Process

But first, there's the process that starts the first time most RHEL 6 systems are booted after installation. And that's the first boot process. While there's a functionally similar text-mode version of the process, the default installation described earlier in this chapter leads to the GUI version of the process. The steps described in this section are based on an installation of the actual RHEL 6; the steps associated with a rebuild distribution will vary.

- 1. It starts with a welcome screen. Click Forward to continue.
- 2. The first boot process continues with a license agreement, which varies depending on whether this is RHEL 6 or a rebuild distribution. (Scientific Linux 6 doesn't even include this step.) If you refuse the license agreement, you're prompted to shut down and remove RHEL 6 from the local system. If you can accept this agreement, select Yes and click Forward to continue.
- 3. You're prompted to connect the system to the RHN. The illustration includes the window that appears if you click Why Should I Connect To RHN.

![](img/9139201cfcaf4292284a0eed074928e5_47_0.png)

- 4. To register, you'll need a RHN account, with an available subscription. As that is not required for the RHCSA/RHCE exams, select No and click Forward to continue.
- 5. You're prompted with the reasons shown in the illustration for registering. To avoid registering at this time, click No Thanks, I'll Connect Later to continue. You can register on the RHN later with the rhn_register command.
- 6. You're prompted with a window that the local system is not set up for software updates. As you'll perform this task in Chapter 7, click Forward to continue.
- 7. While not required for installation, the next step allows you to create a regular user for the system. While you can also connect to a remote database of users, a regular local user is required in this step. If you click Advanced, it opens the Red Hat User Manager, which can help customize user details, as discussed in Chapter 8. Set up at least a local user, and click Forward to continue.
- 8. Now you can set up a date and time for the local system. The date and time that appears reflects that configured in the local hardware. If you select the Synchronize Date And Time Over The Network option, the window changes to show available NTP servers, based on the options associated with the Date/Time Properties tool briefly described in Chapter 5 and covered in detail in Chapter 17. Make desired changes and click Forward to continue.
- 9. Unless you're working with a system with a lot of memory, a message about "Insufficient memory to configure kdump" appears. That system collects data associated with kernel crashes. Click OK or make appropriate changes, and click Finish.

If you haven't installed GUI options such as the GNOME Desktop Environment and the X Window System, you'll see the text-mode alternative to the First Boot tool, as shown in Figure 1-17. Even if the noted GUI options are configured, you can start the equivalent of that tool with the setup command.

It includes six tools. The functionality associated with each of these tools is discussed in several different chapters.

# FIGURE 1-17

The Text-Mode Setup Tool.

![](img/9139201cfcaf4292284a0eed074928e5_48_0.png)

# Default Security Settings

When RHEL 6 is installed, there are default settings associated with SELinux and iptables-based firewalls. As this section just summarizes default settings, it does not include much detail. For more information on these security options, see Chapters 4, 10, and others.

First, SELinux is enabled in enforcing mode by default. You can confirm the setting with the sestatus command, which should lead to the following output:

```
SELinux status:               enabled
SELinuxfs mount:              /selinux
Current mode:                 enforcing
Mode from config file:        enforcing
Policy version:               24
Policy from config file:      targeted
```

You’ll learn more about SELinux and the RHCSA exam in Chapter 4. If you go for the RHCE, you’ll also learn to configure SELinux in Chapters 10 and on to support a wide variety of services.

If you want detailed information about the current iptables command, examine the /etc/sysconfig/iptables file. That file is used by the iptables service, courtesy of the /etc/init.d/iptables script. The following line from that file allows traffic sent through port 22 access from the outside.

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
```

Port 22 is the default port for the Secure Shell (SSH) service, which supports remote administration of the local system. If there’s a good network connection, you’ll be able to connect remotely to this system. If the local IP address is 192.168.122.50, you can connect remotely to user michael’s account with the following command:

```
# ssh michael@192.168.122.50
```

The SSH server can be configured to enhance security even further. For more information, see Chapter 11.

# Special Setup Options for Virtual Machines

On a KVM-based virtual host, you may notice additional firewall rules. For example, in the /etc/sysconfig/iptables file of the virtual host on my system, I see the following additional rule, which accepts traffic over a physical bridged network device.

```
-I FORWARD -m physdev --physdev-is-bridged -j ACCEPT
```

It works for IPv4 networking with the help of active IP forwarding in the dynamic file, /proc/sys/net/ipv4/ip_forward. It's a binary file; if it's set to 1, IPv4 forwarding is active. To set it on a permanent basis, open the /etc/sysctl.conf file, and make sure the following directive is set to 1:

```
net.ipv4.ip_forward=1
```

To implement the changes immediately on the local system, run the following command:

```
# sysctl -p
```

This information is also covered briefly in Chapter 5 in the context of network configuration. A detailed discussion of the related /proc filesystem is a RHCE topic covered in Chapter 12.

# CERTIFICATION OBJECTIVE I.07

# Configure Default File Sharing Services

One of the requirements of the RHCSA guide is to "Configure a system to run a default configuration HTTP server," as well as "Configure a system to run a default configuration FTP server." Let's interpret those statements. The default HTTP server on RHEL 6 is the Apache Web server. The corresponding default FTP server is vsFTP.

While detailed configuration of these services is the province of the RHCE, these systems include basic functionality in their default installations. You'll confirm the operation of the default installation. Next, you'll take this process one step further, to set up these services to share files, specifically the files copied from the installation DVD.
