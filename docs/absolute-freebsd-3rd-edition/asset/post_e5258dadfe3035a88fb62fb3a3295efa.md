
You'll see that a file called *locate.rc* can be found in four places: in the main */etc* directory, the system examples directory, the system source code, and a copy retained by *etcdumpdb(8).*

As part of *periodic(8)'s* weekly run (see Chapter 21), your FreeBSD system scans its disks, builds a list of everything it finds, and stores that list in a database. The list-building program, *locate.updatedb(8),* takes its settings from */etc/locate.rc*. The following variables in this file all change how your *locate.updatedb(8)* builds your locate database:

- *TMPDIR* contains the temporary directory used by *locate.updatedb(8),* and defaults to */tmp*. If you're short on space in */tmp*, change this path to a place where you have more room.
- While you can change the location of the database itself with the *FCODES* variable, this affects other parts of FreeBSD that expect to find that database in its default location. Be prepared for odd results, especially if you leave an old locate database in the default location of */var/db/locate.database*.
- The *SEARCHPATHS* variable gives the directory where you want to start building your database. This defaults to */*, the whole disk. To index only a portion of your disk, set that value here.
- *PRUNEPATHS* lists directories you don't want to index. This defaults to excluding temporary directories that traditionally contain only short-lived files.
- The *FILESYSTEMS* variable lists the types of filesystems you want to index. By default, *locate.updatedb(8)* indexes only UFS (FreeBSD) and *ext2fs* (Linux) filesystems. Listing NFS (see Chapter 13) filesystems is a bad idea: all of your servers simultaneously indexing the fileserver will bottleneck either the network or the fileserver.

## /etc/login.*

You can control who may log into your system—and what resources those users may access—by using */etc/login.access* and */etc/login.conf*. See Chapter 9 for instructions.

## /etc/mail

Most of the contents of `/etc/mail` are dedicated to Sendmail. The two exceptions are the aliases(5) file and mailer.conf(5). We discuss both in Chapter 20.

## /etc/mail.rc

While FreeBSD uses most .rc files for system startup, the `/etc/mail.rc` file is used to configure mail(1).

## /etc/mail/mailer.conf

FreeBSD allows you to choose any mail server program you like via `/etc/mail/mailer.conf`, as covered in Chapter 20.

## /etc/make.conf

To make, or compile, a program is to build it from source code into machine language. We’ll discuss building software in detail in Chapter 17. The `/etc/make.conf` contains settings that control how the building process works, letting you set options that directly affect software builds. Remember, anything you add to make.conf affects all software built on the system, including system upgrades. This may cause upgrade failures. Many of the options from make.conf are useful only to developers.

If you’re interested in setting options that affect only system upgrades, use `/etc/src.conf` instead.

Here are some common features set in make.conf. Any values set here require the same syntax used by make(1). If you insist on trying to optimize software builds, follow the examples in make.conf(5) or in the software’s documentation. Best of all, though, don’t muck with make at all.

### CFLAGS

This option specifies optimization settings for building nonkernel programs. Many other Unix-like operating systems suggest compiling software with particular compiler flags, or CFLAGS. This practice is actively discouraged on FreeBSD. System components that require compiler flags already have that specified in the software configuration, and add-on software has that configuration set for it separately. While people might recommend other settings for CFLAGS, custom options aren't supported by the FreeBSD Project.

In general, FreeBSD code is expected to compile most correctly out of the box. The only thing that adding compiler options can do is impair your performance. If you build FreeBSD or ports with nonstandard flags and have problems, remove those flags and build it again.

### COPTF_FLAGS

The COPTF_FLAGS optimizations are used only for building the kernel. Again, settings other than the defaults can build a nonworking kernel.

### CXXFLAGS

CXXFLAGS tells the compiler what optimizations to use when building C++ code. Be sure to use the += syntax when using CXXFLAGS so that you add your instructions to those specified in the software. Everything that I said earlier about CFLAGS applies equally well to CXXFLAGS.

## /etc/master.passwd

This file contains the confidential core information for all user accounts, as discussed in Chapter 9. Protect it.

## /etc/motd

The message of the day ( motd ) file is displayed to users when they log in. You can place system notices in this file or other information you want shell users to see. The welcome option in /etc/login.conf (see Chapter 9) can point users to different motd files, so you can have separate messages for each login class.

## /etc/mtree

mtree(1) builds directory hierarchies with permissions set according to a predefined standard. The /etc/mtree directory stores that standard for the FreeBSD base system. The FreeBSD upgrade process uses mtree records to install the system correctly. If you damage file or directory permissions in your base system, you can use mtree(1) to restore them to the defaults. While you don’t generally need to edit these files, they can be useful if you muck too much with your system. Diskless systems use these files to build memory-based /var filesystems. We’ll use this information in Chapter 19 to inspect system security.

## /etc/netconfig

If you’re accustomed to SVR4-derived operating systems, you might expect to configure various parts of networking in /etc/netconfig. FreeBSD uses this file only for RPC code, though. I mention it only to keep old Solaris hands from thinking changes here will help them.

## /etc/netstart

This shell script is designed specifically for bringing up the network while in single-user mode. Having a network in single-user mode is terribly useful for any number of reasons, from mounting NFS shares to connecting to remote machines in order to verify configurations. Just run /etc/netstart. This script has no effect when in full multiuser mode.

## /etc/network.subr

This shell script isn't intended for human use; rather, other network configuration scripts use the subroutines defined herein to support common functions.

## /etc/newsyslog.conf

This file configures the rotation and deletion of log files. See Chapter 21 for more information.

## /etc/nscd.conf

The nscd(8) service caches the results of name service lookups to optimize system performance. It's useful if you're running LDAP, but for hostname lookups, you're better off running a local caching resolver.

## /etc/nsm b.conf

FreeBSD's Windows file-share mounting system uses /etc/nsm b.conf to define access to Windows systems, as described in Chapter 13.

## /etc/nsswitch.conf

Name Service Switching is covered in Chapters 8 and 20.

## /etc/ntp/, /etc/ntp.conf

Keeping correct time on your host simplifies . . . well, everything. The time daemon ntpd(8) uses these files, as Chapter 20 illustrates.

## /etc/opie*

*One-time Passwords In Everything* (OPIE) is a one-time password system derived from S/Key. While still used in a few places, it's no longer very popular. You can read opie(4) if you're interested. For the most part, OPIE has been largely replaced by systems like Kerberos, Google Authenticator, and other PAM plug-ins.

## /etc/pam.d/*

*Pluggable Authentication Modules* (PAM) allow the sysadmin to use different authentication, authorization, and access control systems. If you're using Kerberos, LDAP, or some other centralized authentication system, you'll need to configure PAM. PAM, unfortunately, fills an entire book on its own. If you're trapped into going anywhere near PAM, permit me to recommend my book *PAM Mastery* (Tilted Windmill Press, 2016).

## /etc/passwd

This file contains user-visible account information. We talk about the password files in Chapter 9.

## /etc/pccard_ether

This script starts and stops removable network cards, such as Cardbus cards and USB Ethernet. Its name is just a leftover of history, when the only cards available were PC Cards. For the most part, devd(8) runs this script as needed, as discussed in Chapter 13.

## /etc/periodic.conf and /etc/defaults/periodic.conf

The system's regular maintenance jobs that create those annoying mails to root are run by periodic(8), which just runs shell scripts stored in
