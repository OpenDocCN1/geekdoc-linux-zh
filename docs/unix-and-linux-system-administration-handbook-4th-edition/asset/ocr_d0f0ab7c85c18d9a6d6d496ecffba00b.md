Like Solaris, HP-UX includes Darren Reed’s IPFilter package for packet filtering and NAT translation. See IPFilter for UNIX systems on page 939 and Solaris NAT on page 500 for some additional detail. The IPFilter part is all the same, although HP-UX configures the package differently at startup. Instead of using svcadm to enable IPFilter, edit /etc/rc.config.d/ipfconf and turn on the options you want. Configuration files for ipf and ipnat should go in /etc/opt/ipf instead of /etc/ipf.

HP-UX’s version of inetd has built-in TCP wrapper functionality that you configure in the file /var/adm/inetd.sec.

If you wonder in exactly what ways HP has shipped you an insecure system, take a look at Kevin Steves’ article about the steps needed to turn an HP-UX 11 system into a bastion host on an unprotected network: tinyurl.com/5sffy2. This document is a bit old (2002), but it’s an excellent description of all the creature comforts in HP-UX that must be turned off if the machine is to be secure on the open Internet. We wish we knew of a document like this for our other example systems.

# 14.15 AIX NETWORKING

Rather than keeping network configuration information in text files or scripts, AIX squirrels it away in the Object Data Manager (ODM) attribute/value database. Another layer of glue associates these property lists with specific devices (driver instances, really) and binds the drivers to the configuration information.

The Object Data Manager on page 432 describes the ODM system in general. The overall scheme is rather complex, and it allows access to the network configuration at multiple layers. Table 14.13 shows a variety of AIX commands for setting an interface’s network address. They vary chiefly in whether they affect the running configuration, the boot-time configuration, or both.

# Table 14.13 Eight ways to set an interface’s IP address in AIX

| Command | Affects Current? | Affects Boot? |
|---|---|---|
| smitty mk tcpip (and fill out the form) | Yes | Yes |
| mk tcpip -i en3 -a 192.168.0.1 | Yes | Yes |
| chdev -l en3 -a netaddr=192.168.0.1 | Yes | Yes |
| chdev -l en3 -a netaddr=192.168.0.1 -P | No | Yes |
| chdev -l en3 -a netaddr=192.168.0.1 -T | Yes | No |
| ifconfig en3 inet 192.168.0.1 | Yes | No |
| odmchange -o CuAt -q name=en3 AND attribute=-netaddr='config' | No | Yes |
| echo 'Hey! I set the network address!' | No | No |
| a. odmchange requires an attribute/value list as input. You cannot specify attribute values on the command line. | | |