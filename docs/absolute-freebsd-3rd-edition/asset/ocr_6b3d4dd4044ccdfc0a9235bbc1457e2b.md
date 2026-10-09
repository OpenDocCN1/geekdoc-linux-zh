your system management. SNMP version 3 uses encryption to protect data on the wire.

SNMP provides basic security through *communities*. If you go looking around, you'll find all sorts of explanations for why a community isn't the same thing as a password, but a community *is* a password. Most SNMP agents have two communities by default: public (read-only access) and private (read-write access). Yes, there's a default that provides read-write access. Your first task whenever you provision an SNMP agent on any host, on any OS, is to disable those default community names and replace them with ones that haven't been widely documented for decades.

FreeBSD's bsnnmpd(8) defaults to SNMPv2c but can do SNMPv3. SNMPv3 is a more complicated protocol, so we're not going to cover it here. If you understand the SNMPv3 protocol and the basics of configuring FreeBSD's bsnnnpd, you won't have any trouble enabling SNMPv3 in bsnnnpd.

# Configuring bsnnmpd

Before you can use SNMP to monitor your system, you must configure the SNMP daemon. Configure bsnnnpd(8) in /etc/snmpd.conf. In addition to including the default communities of public and private, the default configuration doesn't enable any of the FreeBSD-specific features that make bsnnnpd(8) desirable.

# bsnnmpd Variables

bsnnmpd uses variables to assign values to configuration statements. Most high-visibility variables are set at the top of the configuration file, as you'll see here:

```
location := "Room 200" contact := "sysmeister@example.com" system := 1 # FreeBSD traphost := localhost trapport := 162
```