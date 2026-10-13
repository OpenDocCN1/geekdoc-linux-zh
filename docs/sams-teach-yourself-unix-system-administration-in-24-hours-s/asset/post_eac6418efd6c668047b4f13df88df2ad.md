
The output of this command was hundreds of lines of compilation and configuration information because at the time of this writing, the binary distributions of most packages were unavailable. As a result, fink automatically switched to a source code distribution, and instead of taking just a minute or two, the install took almost ten minutes to complete—two minutes to download the files, and seven minutes to compile and install.

Installing the helpful text-only Web browser lynx is a similarly easy task with fink install lynx.

- 3. To see what's inside a package, use fink describe pkg. Here's a bit more information on bash, for example:

```
# fink describe bash
Reading package info...
Information about 251 packages read.

bash-2.05-3: The GNU Bourne Again SHell
Bash is an sh-compatible command language interpreter that executes
commands read from the standard input or from a file. Bash also
incorporates useful features from the Korn and C shells (ksh and csh).
.
Bash is ultimately intended to be a conformant implementation of the IEEE
Posix Shell and Tools specification (IEEE Working Group 1003.2).
.
Web site: http://www.gnu.org/software/bash/bash.html
.
Porting Notes:
GNU Bash version 2.05 compiles (and installs correctly after
commenting out the install-info line in doc/Makefile.in)
.
Maintainer: Paul Swenson <pds@mac.com>

Done.
```

- 4. Removing a package with fink is straightforward:

```
# fink remove lynx
Reading package info...
Information about 251 packages read.
dpkg -r lynx
(Reading database ... 3548 files and directories currently installed.)
Removing lynx ...
Done.
```

Once you've uninstalled the package, fink is also smart enough to know that the core archive is still available, so a re-install is quite speedy:

```
# fink install lynx
Reading package info...
```

```
Information about 251 packages read.
dpkg -i /sw/fink/dists/stable/main/binary-darwin-powerpc/web/lynx_2.8.4-1_darwin-powerpc.deb
Selecting previously deselected package lynx.
(Reading database ... 3475 files and directories currently installed.)
Unpacking lynx (from ../lynx_2.8.4-1_darwin-powerpc.deb) ...
Setting up lynx (2.8.4-1) ...
Done.
```

- 5. The fink man page has an extensive discussion of the command options, of course, but Table 8.2 summarizes the key options for everyday use.

Table 8.2 Key Options for fink

| Option | Meaning |
|---|---|
| install pkg | Installs the specified package, and any additional packages that might be required. |
| remove pkg | Removes the specified package from the system. |
| list | Lists all packages—marking those installed with an i and those installed but out-of-date with (i). |
| describe pkg | Describes the specified package in detail. |
| selfupdate | Updates fink itself to the very latest version. |

The fink package is surprisingly sophisticated and quite easy to use, a boon to those Darwin users who might be relatively new to the power—and oddness—of Unix. What I most like about it is that you're shielded from having to dig around on the Web and find packages, because they're already registered in the central fink database. That's a model that the RPM team should follow.

Be aware, however, that fink is unquestionably a work-in-progress and doesn't have the benefit of years of widespread use, so don't be surprised if the version of fink you install is more than a little different from that demonstrated here.

## Package Management in Solaris

Solaris uses its own package management system too, one that's more primitive than RPM in some ways, and easier to use in others. It's certainly easier to work with from the command line, one of my greatest criticisms of the RPM system.

### Task 8.4: Managing Packages in Solaris

Similar to other package management systems, the Solaris pkg package management system lets you query packages, find out what's inside a package, and install new packages.

- 1. To see what packages you have installed, use the pkginfo command. Without any argument it lists everything installed:

```
# pkginfo | head -15
system    AW1mega    MEGA Family SCSI Host Bus Adapter
system    CADP100    Adaptec Ultra160 SCSI Host Adapter Driver
system    CPQnft    Compaq NetFlex Family NIC
system    CPQncr    Compaq Family SCSI HBA
system    CPSmii    Compaq SMART 2/E Family of Array Controller
system    HBAFC    Agilent Fibre Channel HBA Driver
system    MADGfmp    Madge Token Ring Family of NIC
system    WLYXfLp    Buslogic FlashPoint Ultra PCI SCSI
system    NCROS86r    NCR Platform Support, OS Functionality (Root)
application NSCPcom    Netscape Communicator
system    SK98sol    SysKonnect SK-NET Gigabit Ethernet Adapter SK-98xx
system    SKFp    SysKonnect PCI-FDDI Host Adapter
system    SUNW125f    Russian 1251 fonts
ALE    SUNWCSft    Traditional Chinese BIG5 True Type Fonts Package
ALE    SUNW5xmft    Chinese/Taiwan BIG5 X Windows Platform minimum required Fonts Package
```

You can also feed it to grep to search for specific packages:

```
$ pkginfo | grep shell
system    SUNWbash    GNU Bourne-Again shell (bash)
system    SUNWtcsh    Tenex C-shell (tcsh)
system    SUNWzsh    Z shell (zsh)
```

- 2. The full name of a package is rather intimidating in pkg. A typical name is gcc-2.8.1-sol26-sparc-local.gz, which should be interpreted as program-version-os-processor-installation directory.gz.

![](img/5ced0c78d748bd190e9027e5549a362_189_0.png)

> A good starting place to learn about Solaris packages available for download is at Steven Christensen's http://www.sunfreeware.com/.

To install a network application, you need to copy the file onto your Solaris system through whatever means you prefer. Typically, this will be ftp or through a Web browser. We'll use ftp for this example:

```
$ ftp ftp.sunfreeware.com
Connected to ftp.sunfreeware.com.
220 ftp.sunfreeware.com FTP server ready.
Name (ftp.sunfreeware.com:taylor): ftp
331 Guest login ok, send your complete e-mail address as password.
Password:
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
```

```
Using binary mode to transfer files.
ftp> cd /pub/freeware/intel/8/
250 CWD command successful.
ftp> dir sud*
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
-rw-r--r-- 1 steve staff 93934 Nov 23 1999 sudo-1.5.9p4-sol8-intel-local.gz
226 Transfer complete.
ftp> lcd /tmp
Local directory now /tmp
ftp> get sudo-1.5.9p4-sol8-intel-local.gz
200 PORT command successful.
150 Opening BINARY mode data connection for 'sudo-1.5.9p4-sol8-intel-local.gz' (93934 bytes).
226 Transfer complete.
local: sudo-1.5.9p4-sol8-intel-local.gz remote: sudo-1.5.9p4-sol8-intel-local.gz
93934 bytes received in 1.2 seconds (76.79 Kbytes/s)
ftp> quit
221 Goodbye.
```

Now the package is copied from the Net to /tmp, so it's time to install it on the Solaris system.

- 3. Installation of packages is done with pkgadd, but you need to take a simple intermediate step first: unzip the file. Fortunately, that's easy, as you learned last hour, with the command gunzip sudo*gz.

```
# gunzip sudo*gz
# pkgadd -d sudo-1.5.9p4-sol8-intel-local
```

```
The following packages are available:
1 SMCsudo        sudo
                   (i86pc) 1.5.9p4

Select package(s) you wish to process (or 'all' to process
all packages). (default: all) [?,??,q]: all

Processing package instance <SMCSudo> from </tmp/sudo-1.5.9p4-sol8-intel-local>

sudo .. (i86pc) 1.5.9p4 -- Todd Miller

The selected base directory </usr/local> must exist before
installation is attempted.

Do you want this directory created now [y,n,?,q] y
Using </usr/local> as the package base directory.
## Processing package information.
## Processing system information.
```

```
## Verifying disk space requirements.
## Checking for conflicts with packages already installed.
## Checking for setuid/setgid programs.

The following files are being installed with setuid and/or setgid permissions:
/usr/local/bin/sudo <setuid root>

Do you want to install these as setuid/setgid files [y,n,?,q] y
Installing sudo as <SMCsudo>

## Installing part 1 of 1.
/usr/local/bin/sudo
/usr/local/doc/sudo/BUGS
/usr/local/doc/sudo/CHANGES
/usr/local/doc/sudo/COPYING
/usr/local/doc/sudo/FAQ
/usr/local/doc/sudo/HISTORY
/usr/local/doc/sudo/INSTALL
/usr/local/doc/sudo/INSTALL.configure
/usr/local/doc/sudo/PORTING
/usr/local/doc/sudo/README
/usr/local/doc/sudo/RUNSON
/usr/local/doc/sudo/TODO
/usr/local/doc/sudo/TROUBLESHOOTING
/usr/local/man/man5/sudoers.5
/usr/local/man/man8/sudo.8
/usr/local/man/man8/visudo.8
/usr/local/sbin/visudo
[ verifying class <none> ]

Installation of <SMCsudo> was successful.
```

The package is installed, and you can see that even something as simple as the sudo command ends up including 16 different files, mostly stored in the new directory /usr/local/bin/sudo.

- 4. To learn more about a package, use the pkginfo command, but specify a package name on the command line. With the -d flag, pkginfo will also show information about a package before it's installed, a critical capability!

First, the already-installed bash package:

```
# pkginfo SUNWbash
system SUNWbash GNU Bourne-Again shell (bash)
```

Notice here that the output of the command without any arguments is minimally informative. The real value is that it can be used to quickly ascertain if a given package is actually installed on the system or not.
