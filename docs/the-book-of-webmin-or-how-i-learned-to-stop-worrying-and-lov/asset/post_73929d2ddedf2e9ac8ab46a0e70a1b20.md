
## Intrusion Detection

There are a large number of free and commercial intrusion detection systems (IDSs) available for all of the major UNIX variants. An IDS provides an easy method of auditing one or more systems to ensure that they have not been exploited. Most such systems create a database of file identifier keys (usually an MD5 hash or similar strongly encrypted key), which is also encrypted with a passphrase known only to the system administrator. Some systems provide an easy means to store the database on another machine, or it can be written to a floppy or CD for use in a read-only mode, so that even if the machine is violated tampering with the file key database is impossible rather than merely extremely difficult.

Perhaps the most popular IDS for free UNIX systems is Tripwire, which is available in both an Open Source and proprietary version. It is available in package form from many Linux distribution vendors and source downloads for all supported operating systems. Tripwire uses a database of MD5 keys, which is generated on a known secure system. Using a simple cron job, Tripwire can then be run periodically to ensure no unexpected changes have occurred on the system since the last database generation. Using two passphrases, it is possible for Tripwire to prevent unauthorized tampering with the database (for example, a cracker regenerating the database after having modified all of the files needed for future entry).

> **NOTE** *The Open Source variant of Tripwire can be downloaded from [http://www.tripwire.org/]. A thorough reading of the documentation is recommended before attempting to use it, because though it is relatively simple to use, the required steps for initial setup and database generation are not at all obvious.*

Another simple but effective intrusion detection method for systems that use RPM or any other package manager that keeps a database and can verify file integrity is to keep a copy of the package database on another system or stored on read-only media. With this database and a known good installation of the package manager, one can verify all of the system files quickly and easily. The drawback of this method is that it cannot detect new files and modification of files that were not installed from packages. If no proper intrusion detection system is available, this can be a lifesaver in the event of an intrusion on a system that has no complete IDS installed.

Some pitfalls to watch for in the event of an intrusion is that once a cracker has gained access to your system with root privileges, there is nothing to prevent him from modifying the Tripwire or package manager binaries to prevent them from reporting good results even after all of their changes. Such a modification is usually obvious to an experienced administrator, because normal file changes should show up in such checks, and over time those changes will probably not be accurately reported by the cracked IDS or package manager. This problem is most easily worked around by installing secondary versions of these tools and running them against a database stored on read-only media, like a CD or floppy disk with writing disabled. While a cracker with the knowledge to make these changes is rare, it is likely that such ideas will eventually be included in rootkits, making it easy for even the most brain-damaged cracker to thoroughly cover his tracks pretty effectively.

## Proactive Attack Response Tools

There are several new tools designed to recognize common types of attack and respond to them quickly enough to diffuse the attack. There is no single name for such systems, and the way in which they work varies depending on their particular focus. Two such tools are PortSentry and Hogwash.

PortSentry is the most mature of these types of tool and takes a more basic approach to the problem. PortSentry keeps an eye on network connections and watches for a rapid series of abnormal connections that is usually indicative of a network scan. When such a scan is detected the host from which the attack originates is simply blocked using the normal packet filter on the system. PortSentry is made more attractive by the fact that a Webmin module exists to easily administer and configure a PortSentry installation.

**NOTE** PortSentry, like Tripwire, is available in both commercial and Open Source versions. The Open Source release is available for download from [http://www.psionic.com/products/portsentry.html].

A newer entry into the field, Hogwash uses a rule-based system to detect hundreds of known exploit types and can drop those packets without disturbing any other kind of traffic from the host. Hogwash is based on the rule engine of the Snort network intrusion detection system, but adds the ability to respond to the intrusion by dropping or disarming the troublemaking packet by rewriting it to a harmless form.

## 4

## USERMIN: A WEBMIN FOR USERS

![](img/d84604054810a13cacfdac212ebee2f7_64_0.png)

This chapter is a short detour away from Webmin to cover a closely related tool called Usermin. The two tools have a lot in common and are often used together to provide a multi-tiered GUI for users and administrators. The commonalities begin with the fact that both were written and are maintained by Jamie Cameron. They share much of the same code base, and the operation of Usermin closely parallels that of Webmin.

Because the Usermin modules are so closely related to the modules in Webmin, it would be pointless to cover them in detail here. What the chapter will cover is the Usermin Configuration module in Webmin, document the modules that do diverge from similar Webmin modules or simply do not exist in Webmin, and provide some discussions about using Webmin and Usermin in real environments with examples to help make the best use of them. Compared to Webmin, Usermin is severely limited,

but it is just those limitations that make it ideal for a certain class of problem, and so those will be the problems that will be discussed along with how Usermin can help solve them.

## Introduction to Usermin

The differences begin with the intention of each. Webmin is used primarily by system administrators, and it provides unlimited power to the logged-in administrator unless permissions are explicitly restricted. Usermin, on the other hand, is used primarily by system users, and the powers of a logged-in Usermin user are by default limited to only the permissions of a normal user. Specifically, Usermin provides access to a web-based mail client, a Java file manager applet, SSH configuration and client modules, GnuPG encryption and decryption, mail forwarding, changing passwords, cron jobs, and a simplified web-based command shell.

**CAUTION** Usermin prefers to use the PAM authentication mechanism used by most Linux distributions and Solaris. Unfortunately, PAM is not well supported on many UNIX variants, or even all Linux versions. For this reason, Usermin will attempt to fall back to directly using the shadow password file if PAM cannot be used for some reason.

**NOTE** PAM is an acronym for Pluggable Authentication Modules. It allows easier integration of a variety of authentication technologies without requiring all authenticating software to be modified to support each authentication type. Modules are available for a vast array of authentication methods, including LDAP, Kerberos, RSA, and UNIX passwd and shadow files. It is widely deployed on most major Linux distributions and Solaris versions 2.6 and above, and is available as packages or in source form for FreeBSD and HP-UX.

## Usermin Installation

Before you can use Usermin, you will have to install it. Unlike Webmin, at the time of this writing no major Linux distribution or UNIX vendor is including Usermin in its standard installation or offering it as an optional package. This will certainly change in time, and OS vendors may be installing it by the time you read this. Check with your vendor for packages, or simply download it from the Usermin website.

## Checking for the Authen-PAM Perl Module

Installing Usermin is just about like installing Webmin, with the one exception that it is recommended to install the Authen-PAM Perl module before installation of Usermin. So first it will be necessary to check for, and possibly install, this Perl module. The easiest way to check for a Perl module is to use a command like the following:

```
[root@grover root]# perl -e 'use Authen::PAM; print "Success\n"'
```
