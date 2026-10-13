# Table 4-3: Security Applications

| Applications | Description |
|---|---|
| Pluggable Authorization Modules (PAM) | Authentication management and configuration (Chapter 28) |
| Shadow passwords | Password encryption (Chapter 28) |
| Lightweight Directory Access Protocol (LDAP) | User management and authorization (Chapter 28) www.openldap.org |
| authconfig-gtk | Red Hat tool to enable and configure authentication tools: Kerberos, LDAP, and shadow passwords |

Outside users may also try to gain unauthorized access through any Internet services you may be hosting, such as a Web site. In such a case, you can set up a proxy to protect your site from attack. For Linux systems, use Squid proxy software to set up a proxy to protect your Web server (see Chapter 20).

To further control access to your system is to provide secure user authentication with encrypted passwords, a Lightweight Directory Access Protocol (LDAP) service, and Pluggable Authentication Modules (PAM) (see Chapter 28). User authentication can be further be controlled for certain services by Kerberos servers (see Chapter 18). Kerberos authentication provides another level of security whereby individual services can be protected, allowing use of a service only to users who are cleared for access. LDAP and Kerberos are all enabled and configured with authconfig-gtk (Authentication in the System Settings menu or window).

To protect remote connections from hosts outside your network, transmissions can be encrypted. For Linux systems, you can use the Secure Shell (SSH) suite of programs to encrypt any transmissions, preventing them from being read by anyone else (see Chapter 18). The SSH programs are meant to replace the remote tools such as rsh and rcp (see Chapter 15), which perform no encryption.

The IPsec protocol also provides encryption of network transmissions, but integrated into the IP packet structure (see Chapter 17). With IPsec you can both encrypt and authenticate transmissions, ensuring that they were not intercepted and tampered with. With IPsec you can implement Virtual Private Networks (VPN), using encrypted transmissions to connect one local network to another using a larger network like the Internet. Red Hat also provides a third-party solution for VPNs called CPIE (see Chapter 5).

You can find the latest news on security issues at the Red Hat Web site (www.redhat.com) along with other Linux sites like Linux Security (www.linuxsecurity.com), Linux Weekly News (lwn.net), and Linux Today (linuxtoday.com).