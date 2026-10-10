
Please be aware that if you configure your system to masquerade as another, any email sent from your system to your system will be sent to the machine you are masquerading as. For example, in the above illustration, log files that are periodically sent to `root@poodle.redhat.com` by the cron daemon would be sent to `root@mail.redhat.com`.

## 5.6 Controlling Access to Services

As a security measure, most network services are managed by a protective program called a TCP wrapper. The protected services are those listed in `/etc/inetd.conf` that specify `/usr/sbin/tcpd`. `tcpd` can allow or deny access to a service based on the origin of the request, and the configuration in `/etc/hosts.allow` and `/etc/hosts.deny`. By default Red Hat Linux allows all service requests. To disable or limit services you can edit `/etc/hosts.allow`. Here is an example `/etc/hosts.allow` file:

```
ALL: redhat.com *.redhat.com
in.talkd: ALL
in.ntalkd: ALL
in.fingerd: ALL
in.ftpd: ALL
```

This configuration allows all connections from `redhat.com` and `*.redhat.com` machines. It also allows talk, finger, and ftp requests from all machines.

`tcpd` allows much more sophisticated access control, using a combination of `/etc/hosts.allow` and `/etc/hosts.deny`. Read the `tcpd(8)` and `hosts_access(5)` man pages for complete details.

## 5.7 Anonymous FTP

Setting up anonymous FTP is simple. All you need to do is install the `anon-ftp` rpm package (which you may have already done at install time). Once it is installed, anonymous FTP will be up and running.

There are a few files you might wish to edit to configure your FTP server.

- `/etc/ftpass`: This file defines most of the access control for your ftp server. Some of the things that you can do are: set up logical “groups” to control access from different sites, limit the number of simultaneous FTP connections, configure transfer logging, and much more. Read the `ftpaccess` man page for complete details.

- `/etc/ftphosts`: The `ftphosts` file is used to allow or deny access to certain accounts from various hosts. Read the `ftphosts` man page for details.

- `/etc/ftpusers`: This file lists all the users that are **not** allowed to ftp into your machine. For example, `root` is listed in `/etc/ftpusers` by default. That means that you can **not** ftp to your machine and log in as `root`. This is a good security measure, but some administrators prefer to remove `root` from this file.

## 5.8 World Wide Web Server

If you installed the Apache web server (from the `apache` package), then your Web service is already up and running! Just point Red Baron (or any other web browser) at `http://localhost`.

The default page shown is `/home/httpd/html/index.html`. You can edit this file (or completely replace it) to your liking. All the CGI programs, icons, and html pages are stored in `/home/httpd`, but this can be changed in the apache configuration files, all of which are stored in `/etc/htpd/conf`. Logs of all htpd activity are kept in `/var/log/htpd`. Setting up your web site is as easy as adding your own HTML pages and links to the `/home/htpd/html/` directory. For more information on customizing your web server we recommend a reference such as **HTML: The Definitive Guide** by Chuck Musciano & Bill Kennedy, published by O’Reilly & Associates.

## 5.9 NFS Configuration

NFS stands for Network File System, and is a way to share files between machines as if they were on your local hard drive. Linux can be both an NFS server and an NFS client, which means that it can “export” filesystems to other systems, and “mount” filesystems exported from other machines.

### 5.9.1 Mounting NFS Filesystems

Use the mount command to mount a NFS filesystem from another machine:

```
mount porky:/mnt/export /mnt/local
```

In this command, `porky` is the hostname of the NFS file server, `/mnt/export` is the filesystem that `porky` is exporting, and `/mnt/local` is a directory on my local machine where I want to mount the filesystem. After the mount command runs (and if I had the proper permissions from `porky`) - voila! - I can enter 'ls /mnt/local' and get a listing of the files in `/mnt/export` on `porky`.

### 5.9.2 Exporting NFS Filesystems

The file that controls what filesystems you wish to export is “/etc/exports”. Its format is:

```
directory hostname(options)
```

the “(options)” are optional. For example:

The following will also work:

```
killall -HUP rpc.nfsd rpc.mountd
```

See the following man pages for more details: `nfsd(8)`, `mountd(8)`, and `exports(5)`. Another good reference is *Managing NFS and NIS Services* by Hal Stern, published by O'Reilly & Associates.

## 5.10 Running Programs at Boot Time

The file `/etc/rc.d/rc.local` is executed at boot time, after all other initialization is complete, and whenever you change runlevels. You can add additional initialization commands here. For instance, you may want to start up additional daemons, or initialize a printer. In addition, if you require serial port setup, you can edit `/etc/rc.d/rc.serial` and it will be executed automatically at boot time.

The default `/etc/rc.d/rc.local` simply creates a nice login banner with your kernel version and machine type.

## 5.11 Color ls Setup

Color ls is now part of the standard `ls` command. To use color-ls simply issue the command (in `bash`):

```
alias ls='ls --color'
```

## 5.12 NIS/NYS Setup

The basic content of this section was donated by Grant Taylor. It was edited for clarity and space. Other content was contributed by users on the `redhat-list` mailing list.

This text attempts to describe the yp, NIS, and NIS+ support offered in Red Hat Linux products.

- What is yp? NIS? NIS+? NYS? These questions are answered in the NIS-HOWTO. It is included with Red Hat Linux in the ldap package and on the CD. If you install the `ldap` package, you will find the NIS-HOWTO in `/usr/doc/HOWTO`.

  The quick answer is that while yp ("Yellow Pages") is the phone book in Britain, NIS is the traditional RPC-based implementation for sharing passwd, group, hosts, services, and other useful things between many machines. NIS+ is a snazzier, and more secure implementation of the same idea. NYS is the public domain version of NIS.

- What is offered? Red Hat ships NYS client code in its libc and plain yp/NIS client programs like ypcat and ypbind. We ship a plain NIS server daemon, since the NYS (aka NIS+) server daemon is not yet ready for prime-time. Our ypserver does not appear to have the tcp_wrapper-style `/etc/hosts.allow/deny` checking compiled in.

- How do I get ypbind to work properly? How do I set up a client workstation? The NYS code in libc does it all. There is no need to run ypbind. You probably *do* need to run domainname (appropriately for the benefit of plain NIS client programs). You must configure which maps are read from where in `/etc/nsswitch.conf`, and which NIS server and domain you are in using `/etc/yp.conf`. nsswitch.conf is well commented, and yp.conf will look like this:

  ```
  domain foo
  ypserver foo.bar.com
  ```

  Do not put the usual `+:::` lines at the end of passwd or group.

- How do I run ypserver (master)? Red Hat ships a plain NIS (a.k.a. yp) server. It works just like any other ypserver—modify the Makefile in `/var/nis` to taste, perhaps move the source files into `/var/nis/src`, or perhaps not, run make to make the databases, and run ypserver. Further documentation is in `/usr/doc/ypserver/*`.

- Where are yppasswd and yppasswd? They are not included in Red Hat Linux, but you can obtain the regular NIS distribution and install it yourself without too much hassle. It is available from the places listed in the NIS HOWTO. You have to modify the `pupgate` script that comes with it, even though the README claims it works with the NYS Makefile we ship. We also don't ship a `rcpserver/yppasswd.h`, although we do have the `.x` file. The yppasswd package comes with both so it doesn't matter much. The NYS define should be used, but don't use the `-lssl` library since it is built into our libc.

- This information is miserably incomplete! There is already an NIS-HOWTO that describes how to set things up far better than this document does or should. It is also included with Red Hat Linux in the `ldap` package.
