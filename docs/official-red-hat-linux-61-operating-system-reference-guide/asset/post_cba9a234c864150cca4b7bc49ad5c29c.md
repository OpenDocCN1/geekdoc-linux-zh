
5.  Create your LDAP directory (examples of LDAP entries are provided at the PADL Software website at http://www.padl.com/ldap_examples.html).

6.  Add entries to your LDAP directory with ldapadd or with a script.

7.  Use ldapsearch to see if slapd is working.

8.  At this point, your LDAP directory should exist. The next step is to configure your LDAP-enabled applications so that they can use the LDAP directory.

## 8.9 Configuring Your System to Authenticate Using OpenLDAP

This section provides a brief overview of how to configure your Red Hat Linux system to authenticate using OpenLDAP. Unless you’re an OpenLDAP expert, you will probably need more documentation than is provided here. Please refer to the references provided in Section 8.10, LDAP Resources on the Web for more information.

### 8.9.1 Install the Necessary LDAP Packages

First, you’ll need to make sure that the appropriate packages are installed on both the LDAP server and the LDAP client machines. The LDAP server needs the openldap package.

The LDAP client machines need the following packages installed: openldap, auth\_ldap, nss\_ldap and pam\_ldap.

### 8.9.2 Edit Configuration Files

#### Edit /etc/openldap/slapd.conf

The slapd.conf file, located in /etc/openldap, contains the configuration information needed by your slapd LDAP server. You’ll need to edit this file to make it specific to your domain and your server.

The suffix line names the domain for which the LDAP server will provide information. The suffix line should be changed from:

```
suffix "dc=acmewidgets, dc=com"
```
or
```
suffix "dc=acmeuniversity, dc=org"
```

The rootdn entry is the DN for a user who is unrestricted by the access control or administrative limit parameters set for operations on the LDAP directory. The rootdn user can be thought of as the root user for the LDAP directory. The rootdn line needs to be changed from:
```
rootdn "cn=root, dc=your-domain, dc=com"
```
to something like:
```
rootdn "cn=root, dc=redhat, dc=com"
```
or
```
rootdn "cn=ldapmanager, dc=my_organization, dc=org"
```

Change the rootpw line from:
```
rootpw secret
```
to something like
```
rootpw {crypt}$4l9sOIJo4kBM
```

In the above example, you’re using an encrypted root password, which is a much better idea than leaving a plain text root password in the `slapd.conf` file. To make this crypt string, you should either copy it out of a `passwd` file, or use Perl:
```
perl -e "print crypt('passwd','a_salt_string');"
```
In the previous Perl line, `salt_string` is a two character salt, and `passwd` is the plain text version of the password.
You could also copy a `passwd` entry out of `/etc/passwd`, but this won’t work if the `passwd` entry is an MD5 password (the default in Red Hat Linux 6.2).

#### Edit `ldap.conf`

Edit the `ldap.conf` files in `/etc` and in `/etc/openldap` on the LDAP server and clients.

Edit /etc/ldap.conf, the configuration file for nss_ldap and pam_ldap, to reflect your organization and search base. The file /etc/openldap/ldap.conf is the configuration file for the command line tools like ldapsearch, ldapadd, etc., and it will also need to be edited for your LDAP setup. Client machines will need to have both of these files modified for your system.

#### Edit /etc/nsswitch.conf

To use nss_ldap, you'll need to add ldap to the appropriate fields in /etc/nsswitch.conf. (Be very careful when editing this file; be sure that you know what you're doing.) For example:

```
passwd: files ldap
shadow: files ldap
group: files ldap
```

#### Copy the PAM Configuration Files

To use pam_ldap, you'll need to copy the PAM configuration files from /usr/doc/nss_ldap>version>/pam.d/ to your /etc/pam.d/ directory. These are a set of PAM configuration files that allow all of the standard PAM-enabled applications to use LDAP for authentication. (PAM is beyond the scope of this LDAP overview, so if you need help, consult Section 2.6, User Authentication with PAM and/or PAM man pages.)

### 8.9.3 Migrate Your Old Authentication Information to LDAP Format

The /usr/share/openldap/migration directory contains a set of shell and Perl scripts for migrating your old authentication information into LDAP format. (Yes, you'll need to have Perl on your system to use these scripts.)

First, you'll need to modify the migrate_common.ph file so that it reflects your domain. The default DNS domain should be changed from:

```
$DEFAULT_MAIL_DOMAIN = "padi.com";
```

to something like:

```
$DEFAULT_MAIL_DOMAIN = "your_company.com";
```

The default base should also be changed, from:

```
$DEFAULT_BASE = "dc=padl,dc=com";
```

to something like:

```
$DEFAULT_BASE = "dc=your_company,dc=com";
```

Next, you’ll need to decide which script to use. The following table should tell you:

| Existing name service | Is LDAP running? | Use this script: |
| :--- | :--- | :--- |
| /etc flat files | yes | migrate_all_online.sh |
| /etc flat files | no | migrate_all_offline.sh |
| NetInfo | yes | migrate_all_netinfo_online.sh |
| NetInfo | no | migrate_all_netinfo_offline.sh |
| NIS (YP) | yes | migrate_all_nis_online.sh |
| NIS (YP) | No | migrate_all_nis_offline.sh |

Run the appropriate script based on your existing name service.
The README and the migration-tools.txt files in /usr/share/openldap/migration provide more details.

## 8.10 LDAP Resources on the Web

Lots of useful information about LDAP can be found on the Web. Please review these sources, especially the OpenLDAP website and the LDAP HOWTO, before you start to set up LDAP on your system.

**OpenLDAP**
http://www.openldap.org

**University of Michigan**
http://www.umich.edu/~dirsrvcs/ldap/

**The SLAPD and SLURPD Administrator's Guide**
http://www.umich.edu/~dirsrvcs/ldap/doc/guides/slapd

**Innosoft/Critical Angle**
http://www.innosoft.com/ldapworld

**Jeff Hodges' LDAP Road Map and FAQ**
http://www.kingsmountain.com/ldapRoadmap.shtml

**PADI (nss_ldap, pam_ldap and ypldapd)**
http://www.padl.com/

**auth_ldap**
http://www.rudedog.org/auth_ldap/1.4/auth_ldap.html

**The LDAP HOWTO**
http://www.linixdoc.org/HOWTO/LDAP-HOWTO.html

**Sendmail 8.[89].x using LDAP to do address lookups**
http://www.stanford.edu/~bbense/Inst.html

**Using a personal LDAP server, the Apache Web server and PHP to manage your personal e-mail addressbook**
http://www.webtechniques.com/archives/1999/05/junk/junk.shtml

Also, remember that man pages exist for the various LDAP daemons and utilities. Please check the man pages if you need more information.

# Part II Installation-Related Reference

# 9 Preparing for a Text Mode Installation

## 9.1 Things You Should Know

Before attempting to install Red Hat Linux, you should collect some system information in order to prevent any surprises during the installation. You can find most of this information in the documentation that came with your system, or from the system’s vendor or manufacturer.

The most recent list of hardware supported by Red Hat Linux can be found at http://www.redhat.com/hardware. It’s a good idea to check your hardware against this list before proceeding.

### Please Note
You can perform a text mode installation of Red Hat Linux 6.2 by following instructions in this chapter and in Chapter 10, *Installing Red Hat Linux via Text Mode*. However, if you’re installing from a CD-ROM, you might prefer to use the graphical installation mode, which offers both ease of use and a flexible, custom-class installation mode. For more information on graphical installations, turn to the *Official Red Hat Linux Installation Guide*.

### Tip
At the end of the *Before You Begin* chapter in the *Official Red Hat Linux Installation Guide* is a table for you to fill out with your specific system requirements, which will help you keep up with any information you will need during your installation.
