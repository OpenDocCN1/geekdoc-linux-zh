```
Interesting ports on 192.168.0.6:
(The 1654 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
111/tcp   open  rpcbind
32771/tcp open  sometimes-rpc5
Device type: general purpose
Running: Linux 2.4.X/2.5.X
OS details: Linux 2.5.25 - 2.5.70 or Gentoo 1.2 Linux 2.4.19 rc1-rc7)
Uptime 5.015 days (since Wed Apr 10 20:41:00 2004)
(1 lines deleted...)
Nmap run completed -- 9 IP addresses (3 hosts up) scanned in 167.191 seconds
```

As you can see, *nmap* displays the names of the open ports and hazards a guess at the operating system name and version number.

# ## Nessus

The Nessus Security Scanner is a modular security auditing tool that uses plugins written in the Nessus scripting language to test for a wide variety of network vulnerabilities. Nessus uses a client-server software architecture with a server called *nessusd* and a client called *nessus*.

![](bbox=[0.13, 0.5, 0.23, 0.58])

Before you try to install Nessus, you must install the *sharutils* RPM. That package includes the *udecode* utility that the Nessus installation script needs. The *sharutils* package isn't installed with any of the standard package groups, so you have to install it yourself.

To install *sharutils*, mount the companion DVD and install it with the following commands:

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh sharutils*.rpm
```

To download and install Nessus, follow these steps:

+   1. **Read the instructions at www.nessus.org/download.html.** Then follow the link to the package you want to download. Follow the instructions and download the files `nessus-installer.sh` and MD5.
+   2. **Type the following command to install Nessus (you must have the development tools, including the GIMP Toolkit, installed):**
+      ```
+      sh nessus-installer.sh
+      ```
+      Respond to the prompts from the installer script to finish the installation. You can usually press Enter to accept the default choices.