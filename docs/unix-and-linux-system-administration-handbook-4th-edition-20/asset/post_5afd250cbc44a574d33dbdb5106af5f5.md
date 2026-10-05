
## Specifics for Linux

The logic behind the configuration info being in /etc and the zone in /var is that you are a secondary server for other sites, you do not control the size of the zone files that named write. To avoid potentially filling up the root partition, you will probably want to keep the files in /var. Zones for which you are the primary server can live with the config files (absolute paths in the named.conf file), or they can live in /var/cache/bind, too.

The sample named.conf file does not need to be modified if you want to run a caching-only server. You must add any zones for which you are authoritative, preferably to the supplied named.conf.local file.

The sample files provided by Ubuntu use some of new BIND features to help your servers be good DNS citizens on the network. For example, .com and .net as delegation-only zones to keep your users' types from generating advertising revenue for Verisign through its Site Finder tool. If you don't use private address space (RFC1918) internally, then the RFC1918 zone files prevent others from escaping the local network. Go, Ubuntu!

The directory /usr/share/doc/bind9 contains several useful references. Check out the README.Debian file (even on Ubuntu) to understand the strategy for configuring BIND.

The SUSE installation says what it is doing and produces a reasonable, well-documented server installation. By default, named runs in a chrooted environment /var/lib/named as user and group "named". The installer creates the chroot jail and populates it with all the files needed to run named, even niceties as the UNIX-domain socket for syslog. Extra configuration files (not named.conf) and zone files live in /etc/named.d and are copied to the jail when named is started. If you don't want to run named in jail, modify the line that says

```
NAMED_RUN_CHROOTED="yes"
```

in /etc/sysconfig/named.conf. What all you have to change; the start scripts in /etc/init.d refer to this information and are able to start named in either fashion.

SUSE provides a sample /etc/named.conf file with helpful comments that explain many of the options. SUSE's /etc/named.conf is not world-readable as it is all on other systems. The default file imports a file named named.conf.include, which imports the rnd-access.conf file from /etc/named.d, both of which are readable to the world. It's entirely clear what SUSE has in mind concerning security. rnd is preconfigured to accept control commands from local-SUSE's named.conf file can be used-to run a caching-only server. If you want to serve your zones, put the zone files in the /etc/named.d directory and list your zones' names in the /etc/named.conf.include file.

The ISC BIND documentation lives in /usr/share/doc/packages/bind9.

![](img/579efec8c67772f31ecf34844bbb71a2_731_0.png)

## Chapter 17 DNS: The Domain Name System

Installing RHEL's BIND package puts the binaries in /usr/sbin, puts the man pages in /usr/share/man, adds a user and group called "named", and creates directories for data files. The "named" user has access to the data files through group permissions.

Unlike this change in /etc/sysconfig/named, the named.conf file goes in /etc (as Paul Vissie and God intended), and the zone files go in /var/named. No sample files are provided, and the bindconf package should have them.

## Specifications for Solaris

Solaris 10 ships with BIND 9.3.4-P1, vintage 2007; you should consider upgrade. Solaris is more to use with BIND 9.6.1-P1 (2009). Solaris has always called their network programs in in.progname and named was no exception, so often you couldn't find it for a bug if you was called in.named, and not named. Happ, this is not true and Solaris comes to calling the server plain old named, though the in.named name persists as a link. Link Linux, Solaris uses a service order file /etc/nsswitch.conf to specify how BIND, NIS, NIS+(Solaris 10 only), and the /etc/hosts file interact. Modifying the hosts line in that file

```
hosts: dns
```

causes name resolution to try /etc/hosts first and then DNS. Putting crucial servers eases the chicken-and-egg problems that sometimes occur at boot time before service is available. Solaris's name service is started by the SMF service default. SMF options specify the command-line arguments. Table 17.19 BIND files in Solaris summarizes filenames and locations.

| File | Directory | Description |
| :--- | :--- | :--- |
| resolv.conf | /etc | Library configuration file |
| named | /usr/sbin | Name daemon |
| named-checkconf | /usr/sbin | Checks configuration syntax |
| named-checkpoint | /usr/sbin | Checks zone syntax |
| named.conf | /etc | Configuration file for server |
| nsswitch.conf | /etc | Service switch file |

## Specifications for HP-UX

HP-UX includes BIND 9.3.2, vintage 2005; better! HP-UX provides several sample nsswitch.conf files for various combinations of databases. Copy the one that seems right for your environment to /etc/nsswitch.conf. HP recommends hosts: dns to avoid problems with booting. It's important to be able to configure the network in the boot sequence without looking up names in NIS or DNS inasmuch as services cannot run until the network is up. HP-UX's startup script for name service is in /etc/config/d/namesvr_dns. HP-UX uses well-commented files for just everything in the directory /usr/newconfig, but also, for name service, However it has a couple of ancient commands related to name service: hosts_named, which transforms a hosts file into a zone file, and sig_named, which sends signals to the running process to control it. The /etc/hosts file these days contains localhost and the host itself so runtime is useless. And since BIND 9, rnd must be used to control named, not signals. Table 17.20 summarizes the filenames and locations for HP-UX.

| File | Directory | Description |
| :--- | :--- | :--- |
| resolv.conf | /etc | Library configuration file |
| named | /usr/sbin | Name server daemon |
| lwresd | /usr/sbin | Lightweight resolver daemon |
| named-checkconf | /usr/sbin | Checks config syntax |
| named-checkzone | /usr/sbin | Checks zone syntax |
| named.conf | /etc/namedb | Configuration file for server |
| nswitch.conf | /etc | Switch file |

## Specifics for AIX

AIX ships with BIND 8 and 9, with binaries named8 and named9, respectively. As shipped, named is a link to named8, which is no longer supported by ISC. They ship versions 8.3.3+ and 9.2.1, vintage January 2004. Slight performance difference AIX does not include the named-checkconf and named-zones commands—perhaps they intend the BIND distribution after 2004. The startup scripts for name service under AIX are in /etc/rc.tcpip. We were starting to think these tables of file locations were silly since operating systems have largely converged to standard locations as far as BIND is concerned, but AIX settles that dispute. Table 17.21 on the next page shows the AIX file names and locations.

## Table 17.21 BIND files in AIX

| File | Directory | Description |
| :--- | :--- | :--- |
| resolv.conf | /etc | Library configuration file |
| named8 | /usr/sbin | BIND 9 name server daemon |
| named9 | /usr/sbin | BIND 9 name server daemon |
| named | /usr/sbin | Link to named8 [default] or named9 |
| named.conf | /etc | Configuration file for server |
| netsvc.conf | /etc | Service switch file |
| irs.conf | /etc | Another service switch file |
| NSORDER | environment | Service switch environment variable |

In typical AIX fashion, there are three mechanisms that embody the "service switch" you specify the order in which directory services are consulted. The NSORDER environment variable overrides what is specified in /etc/netsvc.conf, and the contents override what is in /etc/irs.conf.

Not only are three places to worry about, the syntax is slightly different in each one. For example, to select DNS lookup for hostnames in the netsvc.conf file, you would use the value bind, but to do the same thing in the irs.conf file, you dns. The syntax allows you to specify what to do if the preferred service does not find an answer, but of course it's different from the notation used in the nsswitch.conf file of other systems. See Prioritizing sources of administrative information on page 739 for the details on service switches.
