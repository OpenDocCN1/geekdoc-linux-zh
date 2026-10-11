
# 2.8.2 Making an initrd image

An `initrd` image is needed for loading your SCSI module at boot time. If you do not need an `initrd` image, do not make one and do not edit `lilo.conf` to include this image.

The shell script `/sbin/mkinitrd` can build a proper `initrd` image for your machine if the following conditions are met:

- The loopback block device is available.
- The `/etc/conf.modules` file has a line for your SCSI adapter; for example:
  ```
  alias scsi_hostadapter BusLogic
  ```

To build the new `initrd` image, run `/sbin/mkinitrd` with parameters such as this:

```
/sbin/mkinitrd /boot/newinitrd-image 2.2.15
```

Where `/boot/newinitrd-image` is the file to use for your new image, and `2.2.15` is the kernel whose modules (from `/lib/modules`) should be used in the `initrd` image (not necessarily the same as the version number of the currently running kernel).

# 2.8.3 Building a monolithic kernel

To build a monolithic kernel you follow the same steps as building a modularized kernel with a few exceptions.

- When configuring the kernel only answer Yes and No to the questions (don't make anything modular). Also, you should answer No to kmod support and module version (CONFIG_MODVERSIONS) support in the configuration.
- Omit the steps:
  ```
  make modules
  make modules_install
  ```
- Edit lilo.conf and add the line append=nomodules.

# 2.9 Sendmail

A default sendmail.cf file will be installed in /etc. The default configuration should work for most SMTP-only sites (Simple Mail Transfer Protocol). It will not work for UUCP (Unix to UNIX Copy Protocol) sites; you will need to generate a new sendmail.cf if you must use UUCP mail transfers.

> Although SMTP servers are supported automatically, IMAP (Internet Message Access Protocol) servers are not. If your ISP uses an IMAP server rather than an SMTP server, you must install the IMAP package. Without it, your system won't know how to pass information to the IMAP server or retrieve your mail.

To generate a new sendmail.cf, you will need to install m4 and the sendmail source package. Read the README file in the sendmail sources for more details on creating sendmail configuration files. Also, O'Reilly & Associates publishes a good sendmail reference entitled sendmail, by Bryan Costales.

One common sendmail configuration is to have a single machine act as a mail gateway for all the machines on your network. For instance, at Red Hat we have a machine mail.redhat.com that does all our mail. On that machine we simply need to add the names of machines for which mail.redhat.com will handle mail to /etc/sendmail.cw. Here is an example:

```
# sendmail.cw - include all aliases for your machine
# here.
torgo.redhat.com
poodle.redhat.com
devel.redhat.com
```

Then on the other machines, torgo, poodle, and devel, we need to edit /etc/sendmail.cf to "masquerade" as mail.redhat.com when sending mail, and to forward any local mail processing to redhat.com. Find the DH and DM lines in /etc/sendmail.cf and edit them as such:

```
# who I send unqualified names to
# (null means deliver locally)
DRmail.redhat.com

# who gets all local email traffic
DHmail.redhat.com

# who I masquerade as (null for no masquerading)
DMredhat.com
```

With this type of configuration, all mail sent will appear as if it were sent from redhat.com, and any mail sent to torgo.redhat.com or the other hosts will be delivered to mail.redhat.com.

Please be aware that if you configure your system to masquerade as another any e-mail sent from your system to your system will be sent to the machine you are masquerading as. For example, in the above illustration, log files that are periodically sent to root@poodle.redhat.com by the cron daemon would be sent to root@mail.redhat.com.

# 2.10 Controlling Access to Services

As a security measure, most network services are managed by a protective program called a **TCP wrapper**. The protected services are those listed in `/etc/inetd.conf` that specify `/usr/sbin/tcpd`. tcpd can allow or deny access to a service based on the origin of the request, and the configuration in `/etc/hosts.allow` and `/etc/hosts.deny`.

By default Red Hat Linux allows all service requests. To disable or limit services you can edit `/etc/hosts.allow`. Here is an example `/etc/hosts.allow` file:

```
ALL: redhat.com .redhat.com
in.talkd: ALL
in.ntalkd: ALL
in.fingerd: ALL
in.ftpd: ALL
```

This configuration allows all connections from `redhat.com` and `*.redhat.com` machines. It also allows talk, finger, and FTP requests from all machines.

tcpd allows much more sophisticated access control, using a combination of `/etc/hosts.allow` and `/etc/hosts.deny`. Read the `tcpd(8)` and `hosts_access(5)` man pages for complete details.

# 2.11 Anonymous FTP

Setting up anonymous FTP is simple. All you need to do is install the `anon-ftp` RPM package (which you may have already done at install time). Once it is installed, anonymous FTP will be up and running.

There are a few files you might wish to edit to configure your FTP server.

## /etc/ftpaccess

This file defines most of the access control for your FTP server. Some of the things that you can do are: set up local “groups” to control access from different sites, limit the number of simultaneous FTP connections, configure transfer logging, and much more. Read the `ftpaccess` man page for complete details.

## /etc/ftphosts

The `ftp.hosts` file is used to allow or deny access to certain accounts from various hosts. Read the `ftp.hosts` man page for details.

## /etc/ftpusers

This file lists all the users that are *not* allowed to FTP into your machine. For example, `root` is listed in `/etc/ftpusers` by default. That means that you cannot FTP to your machine and log in as `root`. This is a good security measure, but some administrators prefer to remove `root` from this file.

# 2.12 NFS Configuration

NFS stands for Network File System; it is a way to share files between machines as if they were on your local hard drive. Linux can be both an NFS server and an NFS client, which means that it can **export** filesystems to other systems, and **mount** filesystems exported from other machines.

## 2.12.1 Mounting NFS Filesystems

Use the `mount` command to mount an NFS filesystem from another machine:

```bash
mkdir /mnt/local # Only required if /mnt/local doesn't exist
mount bigdog:/mnt/export /mnt/local
```

In this command, `bigdog` is the hostname of the NFS server, `/mnt/export` is the filesystem that `bigdog` is exporting, and `/mnt/local` is a directory on the local machine where we want to mount the filesystem. After the `mount` command runs (and if we have the proper permissions from `bigdog`) we can enter `ls /mnt/local` and get a listing of the files in `/mnt/export` on `bigdog`.

## 2.12.2 Exporting NFS Filesystems

The file that controls what filesystems you wish to export is `/etc/exports`. Its format is:

```text
directory          hostname (options)
```

The `(options)` are discretionary. For example:

```text
/mnt/export       speedy.redhat.com
```

would allow *speedy.redhat.com* to mount `/mnt/export`, but:

```text
/mnt/export speedy.redhat.com(ro)
```

would just allow *speedy* to mount `/mnt/export` read-only. Each time you change `/etc/exports`, you must tell the NFS daemons to examine it for new information. One simple way to accomplish this is to just stop and start the daemons:

```text
/etc/rc.d/init.d/nfs stop
/etc/rc.d/init.d/nfs start
```

Or you can restart the daemons with this command:

```text
/etc/rc.d/init.d/nfs restart
```

The following will also work:

```text
killall -HUP rpc.nfsd rpc.mountd
```

See the following man pages for more details: nfsd(8), mountd(8), and exports(5). Another good reference is *Managing NFS and NIS Services*, by Hal Stern, published by O'Reilly & Associates.

# 2.13 The Boot Process, Init, and Shutdown

This section contains information on what happens when you boot or shut down your Red Hat Linux system.

## 2.13.1 Behind the Scenes of the Boot Process

When a computer is booted, the processor looks at the end of the system memory for the **BIOS** (Basic Input/Output System) and runs it. The BIOS program is written into read-only permanent memory, and is always ready to go. The BIOS provides the lowest level interface to peripheral devices and controls the first step of the boot process.
