# Chapter 17. Kerberos

Whenever the user needs access to a network service, the client software uses the TGT to request a new ticket for that service from the TGS. The service ticket is then used to authenticate the user to that service transparently.

> Warning
The Kerberos system can be compromised by sending a password in plain text. Any user on the network authenticates against a non-kerberos service by sending a password in plain text. Therefore use of non-kerberos services is discouraged. Such services include Telnet and FTP. Use of other encrypted protocols, such as SSH or SSL secured services, however, is acceptable, though not ideal.

This is only a brief overview of Kerberos authentication on a network works, those seeking an in-depth look at Kerberos authentication, should refer to Section 17.7 Additional Resources.

> Note
Kerberos depends on certain network services to work correctly. First, Kerberos requires synchronization between the machines on the network. Therefore, a clock synchronization program should be set up for the network, such as ntp. For configuring ntp, see /usr/share/doc/ntp-<version-number>/index.html for details on setting up Network Time Protocols.
Also, certain aspects of Kerberos rely on the Domain Name Service (DNS), be sure the DNS entries and hosts on the network are all properly configured. See the Kerberos V5 System Administrator's Guide, provided in PostScript and HTML formats in /usr/share/doc/krb5-server-<version-number> for more information.

# 17.4. Kerberos and PAM

Currently, kerberos services do not make use of Pluggable Authentication Modules (PAM) — kerberos services bypass PAM completely. However, applications that use PAM can make use of Kerberos for authentication if the pam_krb5 module (provided in the pam_krb5 package) is installed. The pam_krb5 package contains configuration files that allow services to use login and gdm to authenticate users and obtain initial credentials using their passwords. If access to network services is always performed by kerberos services or services that use GSS-API, such as IMAP, the network can be considered reasonably safe.

Administrators should be careful not to allow users to authenticate to most network services using Kerberos. Many protocols used by these services do not encrypt the password over the network, destroying the benefits of the Kerberos system. For example, users should not be allowed to authenticate using their Kerberos passwords over Telnet.

The next section describes how to set up a basic Kerberos service.

# 17.5. Configuring a Kerberos 5 Server

When you are setting up Kerberos, install the server file. If you need to set up slave servers, the details of setting up relationships between master and slave servers are covered in the Kerberos 5 Installation Guide located in the /usr/share/doc/krb5-server-<version-number> directory.

To configure a basic Kerberos server, follow these steps: