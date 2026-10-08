
## Chapter 16. iptables

system's version of this file. This provides a quick way to distribute sets of iptables rules to multiple machines.

Important

If distributing the /etc/sysconfig/iptables file to other machines, type /sbin/service iptables restart for the new rules take effect.

### 16.5. Additional Resources

Refer to the following sources for additional information on packet filtering with iptables.

### 16.5.1. Installed Documentation

- iptables — Contains a comprehensive description of various commands, parameters, and other options.

### 16.5.2. Useful Websites

- http://netfilter.samba.org — Contains assorted information about iptables, including a FAQ addressing specific problems and various helpful guides by Rusty Russel, the Linux firewall maintainer. The HOWTO documents on the site cover subjects such as basic networking concepts, 2.4 kernel packet filtering, and NAT configurations.
- http://www.linuxnewbie.org/nhf/Security/Iptables_Basics.html — A basic and general look at the way packets move through the Linux kernel, plus an introduction to constructing simple iptables commands.
- http://www.redhat.com/support/resources/networking/firewall.html — This webpage links to a variety of update-to-date packet filter resources.

## Chapter 17. Kerberos

Kerberos is a network authentication protocol created by MIT with symmetric key cryptography to authenticate users to network services — eliminating the need to send passwords over the network. When users authenticate to network services using Kerberos, unauthorized users attempting to gather passwords by monitoring network traffic are effectively thwarted.

### 17.1. Advantages of Kerberos

Most conventional network systems use password-based authentication schemes. Such schemes require a user to authenticate with their username and password. Unfortunately, the transmission of authentication information for many services is unencrypted. For such a scheme to be secure, the network has to be inaccessible to outsiders, and all computers and users on the network must be trusted and trustworthy.

Even if this is the case, once a network is connected to the Internet, it can no longer be assumed that the network is secure. An attacker who gains access using a simple packet analyzer, also known as a packet sniffer, to intercept usernames and passwords in this manner, compromising user accounts and the integrity of the entire security infrastructure.

The primary design goal of Kerberos is to eliminate the transmission of unencrypted passwords across the network. If used properly, Kerberos effectively eliminates the threat packet sniffers would otherwise pose on the network.

### 17.1. Disadvantages of Kerberos

Although Kerberos removes a common and severe security threat, it may be difficult to implement for a variety of reasons:

- Migrating users from a standard UNIX password database, such as /etc/passwd or /etc/shadow, to a Kerberos password database can be tedious, as there is no automated mechanism to perform this task. For more information, refer to question 2.23 in the Kerberos FAQ online at the URL: http://www.nrl.navy.mil/CCS/people/kenh/Kerberos-faq.html.

- Kerberos has only partial compatibility with the Pluggable Authentication Modules (PAM) system used by most servers Red Hat Linux. For more information on this, Section 17.4 Kerberos and PAM.

- For an application to use Kerberos, its source must be modified to make the appropriate calls to the Kerberos libraries. For some applications, this can be quite problematic due to the size of the application or its design. For incompatible applications, changes must be made to the way in which the server and client communicate. Again, this may require extensive programming. Closed source applications that do not have Kerberos support by default are the most problematic.

- Kerberos assumes that you are a trusted user using an untrusted host on an untrusted network. Its primary goal is to prevent plain text passwords from being sent across such a network. However, if anyone other than the proper user has access to the host that issues tickets for authentication—called the key distribution center (KDC)—the entire Kerberos authentication system is at risk of being compromised.

- Kerberos is an all or nothing solution. If you decide to use Kerberos on your network, you must remember that any passwords transferred to a service which does not use Kerberos for authentication are at risk of being captured by packet sniffers. Thus, your network gains no benefit from the use of client. To secure a network with Kerberos, one must either use kerberized versions of all client/server applications which use unencrypted passwords or not use any client/server applications at all.

### 17.2. Kerberos Terminology

Kerberos has its own terminology to define various aspects of the service. Before learning how kerberos works, it is important to learn the following terms.

**ciphertext**: Encrypted data.

**client**: An entity on the network (a user, a host, or an application) that can get a ticket from Kerberos.

**credential cache or ticket file**: which contains the keys for encrypting communications between a user and various network services. Kerberos supports a framework for using other cache types, such as shared memory, but files are more thoroughly supported.

**crypt hash**: One way has to authenticate users. While more secure than plain text, it is fairly easy to decrypt for an experienced challenger.

**GSS-API**: The Generic Security Service Application Program Interface [RFC-2743] is a set of functions that provide security services which clients can authenticate to servers and which servers can authenticate to clients without specific knowledge of the underlying mechanism. If a network service (such as IMAP) uses GSS-API, it can authenticate users.

**key**: Data used when encrypting or decrypting.

**Key Distribution Center (KDC)**: A service that issues tickets.

**keytab**: A file that includes the keys.

**kinit**: The kinit command allows a principal to obtain Ticket Granting Ticket (TGT).

**principal**: A user.

**realm**: A network.

**service**: A program accessed over the network.

**ticket**: A temporary set of credentials that verify the identity of a client for a particular service.

**Ticket Granting Service (TGS)**: A service that issues tickets.

**Ticket Granting Ticket (TGT)**: A special ticket that allows the client to obtain additional tickets.

**encrypted password**: A plain text, human-readable password.

### 17.3. How Kerberos Works

Kerberos differs from other authentication methods. Instead of authenticating each user to each network service, Kerberos uses symmetric encryption and a third party — known as the Key Distribution Center (KDC) — to authenticate users to a suite of network services. Once a user authenticates to the KDC, it sends a ticket specific to back the user's machine and any kerberized service will look for the ticket on the user's machine rather than asking the user to authenticate using a password.

When a kerberized network logs in their workstation, the principal is sent to the KDC in a request for a Ticket Granting Ticket (TGT) from the Ticket Granting Service (TGS). This request can be sent by the login program so that it is transparent to the user or can be sent by the `kinit` program after the user logs in.

The KDC checks for the principal in its database. If the principal is found, the KDC tells the TGS to create a TGT, which is encrypted using the user's key and returned to that user.

The login or `kinit` program on the client machine decrypts the TGT using the user's key (which computes from the user's password). The key is used only on the client machine and is not sent over the network.

The TGT is set to expire after certain period of time (usually ten hours) and stored in the client machine's credentials cache. An expiration time is set so that compromised TGT is of use by an attacker for only a short period of time. When the TGT is issued, the user will not have to re-enter their password to the KDC until the TGT expires or they log out and login again.
