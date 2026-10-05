
# DNS sanity checking tools

$ dig @ns1.nameservices.net w3w3.com ns
;; QUESTION SECTION:
;w33.com IN NS

;; AUTHORITY SECTION:
92152 IN NS M.GTLDD-SERVERS.NET.
com. 92152 IN NS I.GTLDD-SERVERS.NET.
com. 92152 IN NS E.GTLDD-SERVERS.NET.

The server ns1.nameservices.net has deleted responsibility for w3w3.com by the com servers, but it does not accept that responsibility. It is misconfigured, resulting in a lame delegation. Clients trying to use w3w3.com will get slow service. If w3w3.com is paying nameservices.net for DNS service, they deserve a refund!

Sometimes when you dig at an authoritative server in an attempt to find lame-name, dig returns no information. The query again with the +norecurse flag that you can see exactly what the server in question knows.

# DNS sanity checking tools

Several tools check various aspects of your DNS environment. named-check and named-checkzone are shipped with BIND 9; they check the basic syntax (semantics) of the named.conf file and your zone files. NSD and Unbound-similar tools use nsld-check and unbound-check.

The original DNS checking tool is nslint, written by Craig Leres when he was at Berkeley Berkeley Labs. doc, the domain embassy control program, which checks delegations and finds inconsistencies and errors in your deployed DNS, is discussed in more detail. The tool lamers (from the same web as doc) rifles through logs and sends email to the DNS administrators of offending telling them they have a lame delegation and how to fix the problem. DDT by Jorge Frao and Artur Romao debugs cached data.

dnswalk traverses your delegation and identifies inconsistencies between parent or between forward and reverse records. It also finds missing dots, unnecessary glue records, etc. It is a general DNS hygiene name. dnswalk needs to be able to do zone transfers in order to work its magic.

A DNSSEC debugging and management tools are described on page 663.

doc checks delegations by repeated calls to dig. It reports inconsistencies, errors, and other problems related to a particular domain name. It summarizes the issues that it finds. It also produces a verbose log file in the current directory with details.

# Chapter 17 DNS: The Domain Name System

doc uses the local name server to do its digging. If your domain uses BIND's view statement and includes RFC1918 private addresses in the internal view, running doc on the internal view confuses doc and makes it report spurious errors. If you run doc from outside the domain so that it sees what external users use.

Here's what doc has to say about w3w3.com, the domain above:

```
$ doc w3w3.com
Doc-2.2.3: Starting test of w3w3.com    parent is com.
Doc-2.2.3: Test date - Tue Jul 21 21:15:11 MDT 2009
```

Summary:
ERRORS for w3w3.com. (count: 1)
WARNINGS issued for w3w3.com. (count: 1)
Done testing w3w3.com. Tue Jul 21 21:15:11 MDT 2009

doc puts details of the testing and the errors found (together, over 600 lines) in it log file, in case log.w3w3.com:

> ERROR: NO SOA record for w3w3.com. from ns1.nameserver.net.
doc did not label w3w3.com as a "lame delegation" per se, but that's the underlying problem it. Following the NS records from the parent zone,
checked with ns1.nameserver.net to be sure it was acting as an authoritative name server for w3w3.com; it wasn't.

If you manage a domain that includes subdomains (or don't trust the managers of y parent domain), consider running doc from cron once a week to verify that delegations relating to your domain are correct.

# Performance issues

BIND 9's performance on multiprocessor architectures is not as speedy as developers might have hoped, but several root servers use BIND 9 and happily handle of queries per second. But NSD's and Unbound's performance is probably adequate for most use. Especially for DNSSEC signed zones. We've said this multiple times, but it repeats: set your TTLs to reasonable values—weeks or days, minutes or seconds. The use of short TTL punishes you (because you must constantly reserve the same records) and your clients (because they must constantly fetch them). It also provides attacker with cache poisoning opportunity. Some name servers select TTLs that they don't like (values that seem unreasonably short). Paging degrades server performance, so don't be stingy with hosts that run name servers. You'll need to wait for a week for footprint to stabilize for recursive servers; see page 571.

# VENDOR SPECICS

This section describes the status of name service software on various platforms. Everyone swipes BIND, although you may have to specify that you want it when you install the operating system or install it as a package. Linux distributions are for the most part agile at upgrading to recent releases of BIND. Even so, name service is crucially important. Ubuntu and Red Hat have the entire NSD/Unbound available; SUSE has only in their official repositories. Currently, all of the packaged versions are a bit out of date, so with BIND, you might want to just get the latest source code from ninetlabs and build it yourself.

In this section, we include pointers to the configuration files, the release of BIND on which software is based, and information about how to integrate BIND with other sources as flat files. A more complete discussion of this topic is presented in Chapter 19. In particular, refer to the material beginning on page 739.

We also include pointers to the startup scripts that execute at boot time to start the name service. If name service dies, does not your network, and your web site—everything. Some sites use a keep-running script such as the nanny in the BIND distribution. The entry points are intended for use by system administrators. Do not use inetd or xinetd to manage a server; it restarts the server every time it is needed, dramatically slowing response times and preventing any useful cache being developed.

# Specific for Linux

BIND packages for Linux install a startup script for named that runs through /etc/init.d/bind9 for Ubuntu and /etc/init.d/named for RHEL and SUSE. Linux's named packages install all things in the usual places. Table 17.18 shows the details. Red Hat has some extras that interact with their Network Manager ![](img/579efec8c67772f31ecf3484bbb71a2_729_0.png)

# Chapter 17 DNS: The Domain Name System

tool through a -D command-line flag to named. Details can be found in the doc/README-DBUS file in the Red Hat BIND package.

# Table 17.18 BIND files in Linux

| File | Directory | Description |
| :--- | :--- | :--- |
| resolv.conf | /etc | Resolver library configuration file |
| named.l | /usr/sbin | Name server daemon |
| lwresd | /usr/sbin | Lightweight resolver |
| named.conf | /etc /etc/bind | named config file (RHEL and SUSE) config file (Ubuntu) |
| named-checkconf | /usr/sbin | Checks the syntax of the config file |
| named-checkzone | /usr/sbin | Checks the syntax of zone files |
| namedGetForwards | /usr/sbin | Red Hat only, for Network Manager tool |
| namedSetForwards | /usr/sbin | Red Hat only, for Network Manager tool |
| nsswitch.conf | /etc | Service switch file |

DNS uses a switch file, /etc/nsswitch.conf, to specify hostname-to-IP address mappings should be performed and whether DNS should be tried first, last, or not at all. If no switch file is present, the default behavior is:

- hosts: dns [UNAVAIL=return] files

The UNA clause means that if DNS is available but a name is not found, the lookup attempt should fail rather than continuing to the next entry (in this case, /etc/hosts file). If no server is running (it may be the case during the boot process), the lookup process would consult the hosts file.

Our example distributions all provide the following nsswitch.conf entry:

- hosts: files dns

There is no “best” way to configure the lookups—it depends on how your site is managed. In general, we prefer to keep as much information as possible in DNS rather than in NIS or flat files, but we try to preserve the ability by falling back to the static hosts file during the boot process if necessary.

Ubuntu is the most-to-date of our Linux distributions, with its distributed package being a few months old. Programs and files have one root owner and group “bind” with permissions to allow access if named is invoked as “bind” instead of root.

Some useful files are stored in /etc/bind. Included are a named.conf and zone files for root hints, localhost, the broadcast addresses, and private address space. The supplied named.conf includes the files named.conf.options and named.local. It sets BIND’s default directory to /var/cache/bind; as shipped, the directory exists but is empty.
