
# Security-enhanced Linux (SELinux)

SELinux implements MAC for Linux systems. Although it has gained a foothold in a few distributions, it is notoriously difficult to administer and troubleshoot. This un unattributed quote from a former version of the SELinux Wikipedia page vents the frustration felt by many sysadmins:

> "Intriguingly, although the stated raison d’être of SELinux is to facilitate the creation of individualized access control policies specifically attuned to organizational data custodianship practices and rules, the supportive software tools are so sparse and unfriendly that the vendors survive chiefly on ‘consulting’, which typically takes the form of incremental modifications to boilerplate security policies."

Despite the administrative complexity of SELinux, its adoption has been slowly growing, particularly in environments, such as government agencies, with strict security requirements. Of our example Linux distributions, Red Hat Enterprise Linux has the most mature SELinux model. SELinux is available as an optional package for Ubuntu and SUSE.

Policy development is a complicated topic. To protect a new daemon, for example, a policy must carefully enumerate all the files, directories, and other objects to which the process needs access. For complicated software like sendmail or Apache http, this task can be complex. Least one company offers a 3-day class on policy development.

Fortunately, many general policies are available on-line, and most distributions with reasonable defaults. These can easily be installed and configured for your particular environment. A full-blown policy editor aims to ease policy application can be found at seedit.sourceforge.net.

SELinux has been present in Red Hat Enterprise Linux since version 2.4. A default installation of RHEL enables SELinux protection out of the box.

```
/etc/selinux/config controls the SELinux configuration. The interesting lines are
```

```
SELINUX=enforcing
SELINUXTYPE=targeted
```

The first line has three possible values: enforcing, permissive, or disabled. The enforcing setting ensures that the loaded policy is applied and prohibits violations. permissive allows violations to occur but logs them through syslog, which is valuable for debugging. disabled turns off SELinux entirely.

SELINUXTYPE refers to the type of policy to be applied. Red Hat has two types: targeted, which defines additional security for daemons that Red Hat has protected, and strict, which protects the entire system. Although the strict policy is available, it is not supported by Red Hat; the restrictions are so that

- 6. The protected daemons are httpd, dhcpd, mailman, named, portmap, nscd, nntpd, mysql, postgres, squid, winbindd, and ybind.

## Chapter 22 Security

the system is difficult to use. The targeted policy offers protection for important network daemons without affecting general system use, at least in theory. Even the targeted policy isn't perfect. If you're having problems with newly installed software, check /var/log/messages for SELinux errors.

SUSE uses Novell's implementation of MAC, called AppArmor. However, as version 11.1, SUSE also includes basic SELinux functionality.

Ubuntu ships with AppArmor by default. SELinux packages are maintained by Ubuntu by Russell Coker, the Red Hat bloke who generated the targeted strict policies.

## 22.10 CRYPTOGRAPHIC SECURITY TOOLS

Many of the UNIX protocols in common use from a time before the wide deployment of the Internet and modern cryptography. Security was simply not a factor in the design of many protocols; in others, security concerns were waived away with the transmission of a plaintext password or a vague check to see if packets originated from a trusted host or port.

These protocols now themselves operating in the shark-infested waters of large corporate LANs and the Internet, where, must be assumed, all traffic is open to inspection. Not only that, but there is little to prevent anyone from interfering in network conversations. How can you be sure you're really talking to?

Cryptography solves many of these problems. It has been possible for a long time to scramble messages so that an eavesdropper cannot decipher them, but this is just the beginning of the wonders of cryptography. Developments as public key cryptography and secure hashing have promoted the design of cryptystems that meet any conceivable need.

An excellent resource for those interested in cryptography is RSA Laboratories' Frequently Asked Questions about Today's Cryptography, available for free at rsa.com/rslabs. Despite the name, it is a book-length downloadable in PDF format. The document hasn't been updated since 2000, but most of the information remains valid. Additionally, Stephen Levy's book Crypto is a comprehensive guide to the history of cryptography.

## Kerberos: a unified approach to network security

The Kerberos system, designed at MIT, attempts to address some of the issues of network security in a consistent and extensible way. Kerberos is an authentication system, a facility that "guarantees" that users and services are in who they claim to be. It does not provide any additional security or encryption beyond.

Kerberos uses DES to construct nested sets of credentials called "tickets." Tickets are passed around the network to verify your identity and give you access to network services. Each Kerberos site must maintain at least one physically machine (called the authentication server) to run the Kerberos daemon. This daemon issues tickets to users or services that present credentials, such as passwords, when they request authentication.

In essence, Kerberos improves upon traditional password security in only two ways: it never transmits unencrypted passwords on the network, and it relieves users from having to type passwords repeatedly, making password protection of network services somewhat more palatable.

The Kerberos community boasts one of the most lucid and enjoyable documents ever written about a cryptosystem, Bill Bryant’s "Designing an Authentication System: a Dialogue in Four Scenes."It’s required reading for anyone interested in cryptography and is available at web.mit.edu/kerberos/www/dialogue.html

Kerberos offers a better network security model than the "ignoring security entirely" model, but it is neither perfectly secure nor easy to install. Unfortunately (and perhaps predictably), the Kerberos system distributed as part of Windows Directory uses proprietary, undocumented extensions to the protocols. As a result, it does not operate well with distributions based on the MIT code. Fortunately, the winbind module lets UNIX and Linux systems interact with Active Directory. See Kerberos for Active Directory integration on page 1156 for more information.

## PGP: Pretty Good Privacy

See page 763 for more information about email privacy. Phil Zimmermann’s PGP package provides a tool chest of bread-and-butter utilities focused primarily on email. It can be used to encrypt data, to generate signatures, and to verify the origin of files and messages.

PGP has an interesting history that includes lawsuits, criminal prosecutions, and the privatization of portions of the original PGP suite. Kerberos’s file and protocols are being standardized by the IETF under the name Open, and multiple implementations of the proposed standard exist. The GNU project provides an excellent, and widely used implementation known as GnuPG at gnpgup.org. For clarity, we refer to the system collectively as PGP even though individual implementations have their own names.

PGP is perhaps the most popular cryptographic software in use. Unfortunately, the UNIX/Linux version is nuts-and-bolts enough that you have to understand a fair amount of cryptographic background in order to use it. Although you may find PGP useful in your own work, we don’t recommend that you support it for users because it has been known to spark many puzzled questions. We have found the Windows version to be considerably easier to use the gpg command with its 52 different operating modes.
