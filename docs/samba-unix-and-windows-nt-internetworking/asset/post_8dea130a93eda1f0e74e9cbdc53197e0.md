
## Samba Configuration Files

```
CONFIGFILE = $(LIBDIR)/smb.conf          Samba config file
LMHOSTSFILE = $(LIBDIR)/lmhosts          LMHOSTS file
DRIVERFILE = $(LIBDIR)/printers.def      W95 print drivers
SMB_PASSWD = $(BINDIR)/smbpasswd         Password utility
SMB_PASSWD_FILE = 
$(BASEDIR)/private/smbpasswd             Password file
WORKGROUP = <Workgroup Name>             Workgroup
WEBROOT = $(BASEDIR)
```

## Alternate Authentication Methods

```
PAM_FLAGS = -DUSE_PAM                     PAM
PAM_LIBS = -ldl -lpam

AFS_BASE = /usr/afsws                    AFS
AFS_FLAGS = -DAFS_AUTH -I$(AFS_BASE)/include
AFS_LIBDIR = $(AFS_BASE)/lib
AFS_LIBS = -L$(AFS_LIBDIR) -L$(AFS_LIBDIR)/afs \
          -lkauth -lprot -lubik -lauth -lrxkad -lsys \
          -ldes -lrx -llwp -lcom_err \
          $(AFS_LIBDIR)/afs/util.a

DCE_BASE = /opt/dcelocal                DCE
DCE_FLAGS = -DDCE_AUTH -I$(DCE_BASE)/include
DCE_LIBDIR = -L$(DCE_BASE)/lib
DCE_LIBS =

KRB5_BASE = /usr/local/krb5             Kerberos V5
KRB5_FLAGS = -DKRB5_AUTH -I$(KRB5_BASE)/include
KRB5_LIBS = -L$(KRB5_BASE)/lib -ldes425 \
          -lkrb5 -lcrypto -lcom_err
```

## Completing the Installation

When you have completed the install procedure, the Samba component tree will look something like Table 5.4. Before you can start Samba and verify the installation you will need to install the Samba configuration file smb.conf. This file indicates server role, access controls, what shares are available, whether encrypted passwords are required, and general administrative limits. If this is a new Samba installation, you can copy the default smb.conf file from the ./examples subdirectory in the source distribution into the /usr/local/samba/lib directory. This will allow you to start and verify the new installation. We'll cover the details of smb.conf in the next chapter.

## Table 5.4 Sampling of Samba Component Tree

```
/usr/local/samba
Default install tree.
./bin:
Commands.
  addtosmbpass
  convert_smbpasswd
  make_printerdef
  make_smbcodepage
  nmbd
  nmblookup
  rpcclient
  smbclient
  smbd
  smbpasswd
  smbstatus
  smbtar
  swat
  testparm
  testprns

./lib:
  ./codepages
  smb.conf
Codepage directory.
Samba Configuration.

./man:
Man pages.

./private:
SID and passwords.
  MACHINE.SID
  smbpasswd

./swat:
Swat support.
  ./help
  ./images
  ./include

./var:
Logs and lock dir.
  ./locks
  log.nmb
  log.smb

./var/locks:
Lock and PID files.
  STATUS.LCK
  browse.dat
  namelist.debug
  nmbd.pid
  smbd.pid
```

## Operation

At this point, we've completed the installation and must now decide how we want to run the service. The two Samba service daemons, smbd and nmbd, may either be started as running daemons at system boot time or be invoked when needed by inetd. The latter method will conserve system resources in environments where Samba services are lightly used. For high-demand environments, it may be faster to have the services already up and running when they are required.

To start Samba services as always-active daemons at system boot time, add the stanzas listed in Example 5.4 to your /etc/rc.local startup script for BSD UNIX installations or as part of your /etc/rc.d/init.d functions under SYSV UNIX. The commands can also be entered from the command line as root for testing.

### Example 5.4 Samba Daemon Startup

```
/usr/local/samba/bin/smbd -D
/usr/local/samba/bin/nmbd -D
```

To invoke Samba services under inetd, first add the service ports to /etc/services (Example 5.5). Then add the startup stanzas to /etc/inetd.conf (Example 5.5). Note the use of tcpwrappers /usr/sbin/tcpd parameter. It is a good idea to restrict access to the service using a tool like tcpwrappers. Remember that you will have to send a HUP signal to the inetd process to activate these changes in the running system.

### Example 5.5 Samba inetd Startup

# /etc/services

```
netbios-ns      137/udp
netbios-ssn     139/tcp
```

# /etc/inetd.conf

```
netbios-ssn stream tcp nowait root /usr/sbin/tcpd
    /usr/local/samba/bin/smbd smbd
netbios-ns dgram udp wait root /usr/sbin/tcpd
    /usr/local/samba/bin/nmbd nmbd
```

With the Samba smbd and nmbd daemons running, you can verify the services using the nmblookup and smbclient commands. Use nmblookup to query the nmbd name service. You can use your local hostname as an argument. Nmbd should respond with your IP address and hostname (Example 5.6).

### Example 5.6 Samba Name Service Test

```
$ nmblookup wizard
192.168.0.26  wizard
```

Next use smbclient to access your home directory (Example 5.7). You will be prompted for your password. If you have problems getting smbd to accept your password, check the password encryption options defined in smb.conf (Chapter 7).

### Example 5.7 Samba Shares Access Test

```
$ smbclient //wizard/deroest
Password:
Domain = [EYRIE] OS = [Unix] Server = [Samba 2.0.5a]
smb: \>
```

## Summary

- If you are upgrading from a previous release, verify your version using the `smbstatus` or `smbclient` commands and back up your current environment.
- Download Samba distributions from the Samba Web site at http://samba.org.
- Verify the distribution version from the package file name, `samba-<version>.tar.gz`. A version of "latest" indicates the current production release.
- Decide whether to use a binary or source distribution.
- If you will be making local modifications to the source, consider using the GNU Concurrent Versions System (CVS). Refer to http://samba.org/cgi-bin/cvs-web for read-only Web-based access to Samba CVS distributions.
- Extract the distribution package in your source maintenance directory:
  ```
  $ gzip -dc samba-<version>.tar.gz | tar -xvf -
  ```
- If you will be building a pre-version 2.x distribution, edit the Makefile to reflect your operating system configuration.
- Build and install the distribution.
  1. `$ configure` Version 2.x and newer only.
  2. `$ make` Compile.
  3. `$ make install` Install binaries.
- Install a copy of the Samba configuration file `smb.conf` in `/usr/local/samba/lib`. A sample `smb.conf` file can be found in the `./examples` subdirectory of the distribution tree.
- Configure Samba `smbd` and `nmbd` startup either as running daemons or under `inetd` control.
- Start the service and verify with the `nmblookup` and `smbclient` commands.

## Part III: Configuration

## Part Overview

- Chapter 6: Samba Configuration, smb.conf
- Chapter 7: Samba Authentication
- Chapter 8: Name Service
- Chapter 9: Browsing
- Chapter 10: Domains
- Chapter 11: Sharing Files
- Chapter 12: Print Shares

## Chapter 6: Samba Configuration, smb.conf

## Overview

The Samba players have now been fashioned and arrayed upon this, our operating system stage. Time now to tender the libretto, directing the measure of their shares. In other words, we've completed the Samba installation process. Now it's time to direct our attention toward defining the server's role in the workgroup or domain and specify what resources it will share.

In this chapter, we will become familiar with the general structure and syntax of the Samba configuration file, `smb.conf`. This file directs the runtime behavior of both the `smbd` and `nmbd` daemons. In the ensuing Chapters 7 through 12, we'll scrutinize the specific sections and parameters of the Samba configuration file that affect authentication, name service, browsing, domain control, sharing files, and sharing printers. In Chapter 15 we will assess the administrative and event logging parameters that can be specified in `smb.conf`.

Appendix C includes a copy of the default `smb.conf` file that ships with the 2.0.5a release. It may be helpful to refer to this file as we review the configuration file structure and syntax. An online copy of this file can be found in the `./examples` subdirectory of the Samba distribution tree. The file is well documented and can be used as a template for building your own configuration file. Refer to the `smb.conf` (5) manpage for additional information.

```
$ man 5 smb.conf
```
