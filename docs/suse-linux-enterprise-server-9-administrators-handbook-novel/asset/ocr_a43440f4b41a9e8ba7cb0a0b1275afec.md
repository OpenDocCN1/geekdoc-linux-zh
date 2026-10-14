authentication or returns the default directory for the user as well as the list of groups the user belongs to.

In such an environment, users’ home directories are often resident on a single server and made available across the network as exported NFS shares.

In terms of PAM, the standard `pam_unix2` module understands and interacts with the NIS environment.

# Samba Domains

Samba is an implementation of a group of applications that provide for cross-platform file and print services. It is an open source implementation of the Server Message Block (SMB) and Common Internet File System (CIFS). Both of these protocols were originally defined by Microsoft. Unlike the Microsoft implementation of SMB and later CIFS, Samba is available on a multitude of platforms and native operating systems.

Included in the architecture of Samba is the concept of a domain within which users and servers reside. CIFS can be configured to be the primary domain controller (PDC), a secondary (or backup) domain controller (BDC), or simply a member server. In any of these configurations, the authentication process for member SLES servers can be made to point to the central repository of domain accounts.

Unlike NIS, Samba allows for the bridging of the authentication environment across incompatible operating systems such as OpenVMS, Unix, and Windows.

# Lightweight Directory Access Protocol (LDAP)

The Lightweight Directory Access Protocol (LDAP) is a reduced scope implementation of the X.500 directory protocol. LDAP allows for a server or group of servers to share a common repository of information. A typical use for LDAP would be as an address book. Such repositories can contain large volumes of data that need to be accessed in a variety of ways quickly and efficiently. Additionally, LDAP does not demand that all entries contain the same collection of attributes.

As a central store of information, an LDAP server can be accessed by numerous systems simultaneously. Because it is based on an open standard, multiple different applications and platforms can exchange information through a consistent data model. These attributes make LDAP an ideal candidate for sharing account information.