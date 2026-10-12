
## Running Standalone Servers

```
isdn      0:off 1:off 2:on 3:on 4:on 5:on 6:off
dovecot   0:off 1:off 2:off 3:off 4:off 5:off 6:off
network    0:off 1:off 2:on 3:on 4:on 5:on 6:off
tux        0:off 1:off 2:off 3:off 4:off 5:off 6:off
ypbind     0:off 1:off 2:off 3:off 4:off 5:off 6:off
ypserver   0:off 1:off 2:off 3:off 4:off 5:off 6:off
firstboot  0:off 1:off 2:off 3:on 4:off 5:on 6:off
... many lines of output deleted ...
```

The output shows the status of each service for each of the run levels from 0 through 6. For each run level, the service is either on or off. At the very end of the listing, `chkconfig` displays a list of the services that `xinetd` controls. Each `xinetd`-based service is also marked on or off, depending on whether or not `xinetd` is configured to start the service.

> **Note**: You can typically configure services to run under `xinetd` or on a standalone basis. For example, prior to version 8.1, Red Hat Linux started the FTP service under control of `xinetd`. Starting with version Red Hat Linux 8.1 and in Fedora Core, however, the Very Secure FTP server (`vsftpd`) is set up as a standalone server. Nowadays, if you have to start the FTP service, type **service vsftpd start**. To start the FTP service automatically at boot time, type **chkconfig vsftpd on**.

## Using the service configuration utility

If you don't like typing the `chkconfig` commands, you can use a graphical service configuration utility program to configure the services. To run the service configuration utility, log in as **root** and choose Main Menu:*System Settings*:*Server Settings*:*Services from the GNOME or KDE desktop. You can then turn services on or off from the Service Configuration window (as in Figure I-2).

![](img/9f89727199836b0f871f1745838aa8b2_635_0.png)

The service configuration utility shows the names of services in a scrolling list. Each line in the list shows the name of a service with a box in front of the name. A check mark in the box indicates that the service is already selected to start at boot time for the current run level. When the dialog box first appears, many services are already selected.

You can scroll up and down the list and click the box to select or deselect a service. If you click the box, the check mark alternately turns on and off. To find out more about a service, click the service name and a brief description appears in the right-hand side of the window. For example, Figure 1-2 shows the help text for the `atd` service. Additionally, the utility also shows you whether the selected service is currently running or not.

After you select all the servers you want to start when the system boots, click Save on the toolbar to save the changes. Then choose File*Quit to exit.

![](img/9f89727199836b0f871f1745838aa8b2_636_0.png)

By default, the service configuration utility configures the selected services for the current run level. That means if you’re selecting services from the graphical desktop, the system is in run level 5 and the services you configure are set to start at run level 5. If you want to set up the services for a different level, select that run level from the Edit Runlevel menu.

Table 1-1 shows a list of the services, along with a brief description of each one. The first column shows the name of the service, which is the same as the name of the program that has to run to provide the service. You may not see all these services listed when you run the service configuration utility on your system because the exact list of services depends on what is installed on your Fedora Core system.

### Table 1-1: Some Common Services in Fedora Core

| **Service Name** | **Description** |
| :--- | :--- |
| `acpid` | Listens to Advanced Configuration and Power Interface (ACPI) events from the kernel and notifies other programs when such events occur. ACPI events can occur when the kernel puts the computer into a low-power state (for example, standby mode) to save energy. |
| `aep1000` | Loads and unloads the driver for the Accelerated Encryption Processing card called the AEP1000, which can do encryption fast (use this service only if you have the card installed in your system). |
| `anacron` | Executes commands scheduled to run periodically. |
| `apmd` | Monitors the Advanced Power Management (APM) BIOS and logs the status of electric power (AC or battery backup). |
| `atd` | Runs commands scheduled by the `at` and `cron` commands. |
| `autofs` | Automatically mounts file systems (for example, when you insert a CD-ROM in the CD-ROM drive). |
| `bcm5820` | Loads and unloads the driver for Broadcom's BCM5820 CryptoNet SSL (secure sockets layer) accelerator chip (use this service only if you have the hardware installed). |
| `cpuspeed` | Dynamically adjusts the CPU's frequency (the clock speed) and voltage to slow it down in order to conserve power and reduce heat. Controlling the CPU frequency can help increase a laptop computer's battery life and reduce the heat it generates. This daemon is configured through the configuration file `/etc/cpuspeed.conf`. |
| `crond` | Runs user-specified programs according to a periodic schedule the `crontab` command set. |
| `cups` | Runs the Common UNIX Printing System (CUPS) daemon (`cupsd`). |
| `cups-lpd` | Enables applications to use the legacy LPD (line printer daemon) protocol to communicate with CUPS. |
| `finger` | Answers finger protocol requests (for user information, such as login name and last login time). You have to enable `xinetd` for this service to run. |
| `firstboot` | Runs the first time you boot Fedora Core and enables you to set the date and time, create user accounts, and install other CD-ROMs. |
| `gpm` | Enables use of mouse in text-mode screens. |
| `httpd` | The Apache World Wide Web (WWW) server. |
| `innnd` | The InterNetNews daemon — the Internet news server you can use to support local newsgroups on your system. |
| `ipop3` | Allows remote POP3 (Post Office Protocol version 3) clients to download mail messages. You have to enable `xinetd` for this service to run. |
| `iptables` | Automates a packet-filtering firewall with `iptables`. |
| `irda` | Supports communications with IRDA-compliant infrared devices in Linux (IrDA is a standard for infrared wireless communication at speeds ranging from 2400bps to 4Mbps). |
| `irqbalance` | Distributes interrupts to the processors in a multiprocessor system so as to balance the load among the processors. |
| `isdn` | Starts and stops ISDN (Integrated Services Digital Network) services — a digital communication service over regular phone lines (enable only if you have ISDN service). |
| `kudzu` | Probes for new hardware and configures changed hardware. |
| `lisa` | Starts and stops the LAN Information Server (LISA) daemon that can display information about hosts in the local area network (LAN) by broadcasting on TCP port 7741. To find out more about LISA, visit `lisa.home.sourceforge.net`. |
| `messagebus` | Runs the D-BUS daemon that enables applications to receive notification of system events, such as the addition of a new hardware device. To find out more about D-BUS, see `www.freedesktop.org/software/dbus/`. |
| `named` | A server for the Domain Name System (DNS) that translates host names into IP addresses. You can run a copy on your system if you want. |
| `netfs` | Enables you to mount and unmount all network file systems (NFS, Samba, and Netware). |
| `network` | Enables you to activate or deactivate all network interfaces configured to start at system boot time. |
| `nfs` | Enables sharing of file systems specified in the `/etc/exports` file using the Network File System (NFS) protocol. |
| `nfsslock` | Provides file-locking capability for file systems exported using the Network File System (NFS) protocol, so other systems (running NFS) can share files from your system. |
| `ntpd` | The server for Network Time Protocol version 4 (NTPv4) that is used for synchronizing clocks on computers in a network. |
| `pcmcia` | Provides support for PCMCIA devices. |
| `portmap` | Server used by any software that relies on Remote Procedure Calls (RPC). For example, NFS requires the `portmap` service. |
| `postgresql` | Starts or stops the PostgreSQL server that handles database requests. (PostgreSQL is a free database that comes with Fedora Core.) |
| `random` | Server needed to generate high-quality random numbers on the Fedora Core system. |
| `rawdevices` | Assigns raw devices to block devices (needed for applications such as Oracle). |
| `readahead` | Loads into memory programs used during startup before they are needed. This service makes the system start up faster. |
| `rhnxd` | Periodically connects to the Red Hat Network Services servers to check for updates and notifications. |
| `rpc.gssd` | Server that manages the Generic Security Service (GSS) for NFS version 4 clients and provides security for protocols that use Remote Procedure Call (RPC). |
| `rpc.idmapd` | Server that maps user name to user ID and group ID numbers. This is needed to support NFS version 4. |
