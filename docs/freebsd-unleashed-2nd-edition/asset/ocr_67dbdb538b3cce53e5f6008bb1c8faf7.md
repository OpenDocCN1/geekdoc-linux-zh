Samba provides the ability to restrict access on all these levels, as well as to act itself as a “master browser” (in workgroup context) or as a domain controller (the central logon authority in a domain environment). You will see how this is done shortly.

# File and Print Sharing with Macintosh Clients Using AppleTalk

Samba won't provide SMB/CIFS capabilities for communicating with Macintosh clients. For that task, consider AppleTalk. This LAN-level protocol suite operates over its own transport layer or over IP, and it's used by many enterprise and university networks.

The software package that provides AppleTalk functionality to Unix platforms, called netatalk, is available in the ports collection. To install AppleTalk support, build netatalk from the ports at /usr/ports/net/netatalk. (Ignore the netatalk-asun port and install only the basic netatalk port; if you install both ports at once, AppleTalk won't work.)

Enable the NETATALK option in your kernel configuration. See Chapter 16, “Kernel Configuration,” for information on building a custom kernel. The netatalk port installs a number of configuration files—one for each necessary daemon—along with /dist (or distribution) reference copies. The daemons run in the default installed configuration; you can change some of the config files to tweak their behavior. Every Macintosh on the network will see the machine in its AppleShare zone in the Chooser (or in the Connect to Server window in Mac OS X).

See the official netatalk Web site at `http://netatalk.sourceforge.net/` for fuller descriptions of the various tools in the netatalk package and links to other documentation.

# Installing and Configuring Samba

Samba is available in the ports at `/usr/ports/net/samba` or in the packages. Refer to Chapter 14, “Installing Additional Software,” for details on how to install a package or port.

Once you have installed the Samba package, a variety of new items will be installed, including daemon executables (in `/usr/local/sbin`), administrative tools (in `/usr/local/bin`), documentation and examples (in `/usr/local/share`), and configuration files that go into `/usr/local/etc`. Some of the possible config files don't exist in the default installation; you have to create them from scratch if you want to take advantage of their functionality. There are also code pages (in `/usr/local/etc/codepages`) that map Windows character sets to Unix ones.

The only configuration file that exists in the package is `smb.conf.default`, which you must rename to `smb.conf` for it to work. Similarly, the `/usr/local/etc/rc.d/samba.sh.sample` startup script must be renamed to `samba.sh`. In the very easiest way to get Samba running, you only need to edit `smb.conf` and modify the workgroup line to reflect the workgroup or domain of which your machine is a part:

```
# workgroup = NT-Domain-Name or Workgroup-Name, eg: REDHAT4
workgroup = MYGROUP
```