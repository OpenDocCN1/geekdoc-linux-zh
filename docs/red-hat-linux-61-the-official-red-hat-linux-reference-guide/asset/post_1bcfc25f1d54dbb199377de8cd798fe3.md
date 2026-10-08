
# Chapter 13. Lightweight Directory Access Protocol (LDAP)

You will be prompted to type and re-type a password, the program prints the resulting encrypted password to the terminal.

Next, copy the newly created password into the /etc/openldap/slapd.conf on one of the rootpw lines and remove the hash (#).

When finished, the line should look similar to the following example:

```
rootpw {SSH}vv2y+i6V6esasazIv70SSnNAJE18bb2u
```

# Warning

LDAP passwords, including the rootpw directive in /etc/openldap/slapd.conf, are sent over the network in unencrypted, unless you enable TLS encryption.

To enable TLS encryption review the comments in /etc/openldap/slapd.conf and see the man page for slapd.conf.

For added security, the rootpw directive should be commented out after populating the LDAP directory by replacing it with a hash (#).

When using the /usr/sbin/slappadd command line tool locally to populate the LDAP directory, use of the rootpw directive is not necessary.

# Important

You must be the root user to use /usr/sbin/slappadd. However, the directory server runs as the ldap user. Therefore the directory server will not be able to modify any files created by slappadd. To correct this issue, after you have finished using slapp, type the following command:

```
chown -R ldap /var/lib/ldap
```

# 13.7. Configuring Your System to Authenticate Using OpenLDAP

This section provides a brief overview of how to configure a Red Linux system to authenticate using OpenLDAP. Unless you are an OpenLDAP expert, you probably need more documentation than is provided here. Please refer to the references provided in Section 13.9 Additional Resources for more information.

### Install the Necessary LDAP Package

First, you should make sure the appropriate packages are installed on both the LDAP server and the LDAP client machines. The LDAP server needs the openldap-servers package.

The openldap, openldap-clients, and nss_ldap packages need to be installed on all LDAP client machines.

### Edit the Configuration Files

- On the server, edit the /etc/openldap/slapd.conf file on the LDAP server to make sure it matches the specifics of your organization. Please refer to Section 13.6.1 Editing /etc/openldap/slapd.conf for instructions on editing slapd.conf.
- On the client machines, both /etc/openldap/ldap.conf and need to contain the proper server and search base information for your organization.
The simplest way to do this is to run the Authentication Configuration Tool (authconfig-gtk) and select LDAP Support under the User Information tab.
You can also edit these files by hand.
- On the client machines, the /etc/nsswitch.conf must be edited to use LDAP.
The simplest way to do this is to run the Authentication Configuration Tool (authconfig-gtk) and select LDAP Support under the User Information tab.
If editing /etc/nsswitch.conf by hand, add ldap to the appropriate lines.

For example:
password: files ldap
shadow: files ldap
group: files ldap

# 13.7.1. PAM and LDAP

To have PAM-enabled applications use LDAP for authentication, run the Authentication Configuration Tool (authconfig-gtk) and select LDAP Support under the Authentication tab. For more configuring PAM, Chapter 14 Pluggable Authentication Modules (PAM) and the PAM man pages.

# 13.7.2. Migrating Old Authentication Information to LDAP Format

The /usr/share/openldap/migration/ directory contains a set of shell and Perl scripts for migrating information into LDAP format.

First, modify the common.conf file so that it reflects your domain. The default DNS domain should be changed from its default value to something like:

```
$DEFAULT_MAIL_DOMAIN = "your_company";
```

The default base should also be changed, to something like:

```
$DEFAULT_BASE = "dc=your_company, dc=com";
```

The job of migrating a user database into a that is LDAP readable falls to a group of migration scripts installed in the same directory. Using Table 13-1, decide which script to run in order to migrate your user database.

| Existing name service | LDAP running? | Script to Use |
|---|---|---|
| /etc file files | yes | migrate_all_online.sh |
| /etc file files | no | migrate_all_offline.sh |
| NetInfo | yes | migrate_all_netinfo_online.sh |
| NetInfo | no | migrate_all_netinfo_offline.sh |
| NIS (YP) | yes | migrate_all_nis_online.sh |
| NIS (YP) | no | migrate_all_nis_offline.sh |

Table 13-1. LDAP Migration Scripts

Run the appropriate script based on your existing name service.

> Note
> You must have Perl installed on your system to use some of these scripts.

The README and the migration-tools.txt files in the `/usr/share/openldap/migration/` provides more details on how to migrate the information.

# 13.8. Upgrading to OpenLDAP Version 2.0

In OpenLDAP Version 2.0, the on-disk storage format used by the `ldap` LDAP server has changed. If you are upgrading LDAP from Red Linux 7.0 or earlier, you will need to extract the directory command to import this change into an LDIF file using the following:

```
ldbmcat -n > <ldif_file>
```

In the above command, change `<ldif_file>` to the name of the output file. Next type the following command to import this file into OpenLDAP 2.0:

```
slappadd -l <ldif_file>
```

> Important
> You be the root user to use `/usr/sbin/slappadd`. However, the directory server runs as the `ldap` user. Therefore the directory server will not be able to modify any files created by `slappadd`. To correct this issue, after you finished using `slappadd`, type the following command:

```
chown -R ldap /var/lib/ldap
```

# 13.9. Additional Concerning Resources

More information concerning LDAP is available. Please review these sources, especially the OpenLDAP website and the LDAP HOWTO, before configuring LDAP on your system.

# 13.9.1. Installed Documentation

- LDAP man pages — The ldap page provides a good introduction to LDAP. Man pages also exist for the various daemons and utilities.
- /usr/share/docs/openldap-<versionnumber> Contains a general README document and miscellaneous information.

# 13.9.2. Useful Websites

- http://www.ldap.org/ Home of the OpenLDAP Project. This website contains a wealth of information about configuring OpenLDAP.
- http://www.redhat.com/mirrors/LDAP/HOWTO/LDAP-HOWTO.html An older, but still relevant LDAP HOWTO.
- http://www.padl.com/ Developers of nss_ldap and pam_ldap, among other useful LDAP tools.
- http://www.kingsmountain.com/ldapRoad.shtml Jeff Hodges' LDAP Map links to several useful FAQs and emerging news concerning the LDAP protocol.
- http://www.webtechniques.com/archives/2000/05/wilcox A useful look at managing groups in LDAP.
- http://www.ldapman.org/articles Articles that offer a good introduction to LDAP, including methods to design a directory tree and customizing directory structures.

# 13.9.3. Related Books

- Implementing LDAP by Mark Wilcox; Wrox Press, Inc.
- Understanding and Deploying LDAP Directory Services by Tim Howes et al.; Macmillan Technical Publishing

# III. Security Reference

Using secure protocols is a critical part of maintaining system integrity. This part describes critical tools used for the purpose of user authentication, network access control, secure network communication, and intrusion detection. For more information about securing a Red Hat Linux system, refer to the Red Hat Linux Security Guide.

# Table of Contents

+ 14. Pluggable Authentication Modules (PAM) ................................................................ 197
+ 15. TCP Wrappers and xinetd.................................................................................. 205
+ 16. iptables............................................................................................................... 219
+ 17. Kerberos........................................................................................................................ 229
+ 18. SSH Protocol.............................................................................................................. 237
+ 19. Tripwire...................................................................................................................... 245
