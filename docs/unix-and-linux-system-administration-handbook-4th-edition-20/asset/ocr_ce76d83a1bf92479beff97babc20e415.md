# OpenLDAP: the traditional open source LDAP server

UNIX; and now "Windows Server 2008 UNIX Interoperability Components" that facilitate the mapping of UNIX users and groups. See Chapter 30, Operating with Windows, for more information about integrating your UNIX systems with Active Directory-based LDAP.

# LDAP documentation and specifications

A good general introduction to LDAP is LDAP for Rocket Scientists, which covers LDAP architecture and protocol. Find it on-line at zytrax.com/books/ldap. Another other good source of information is the LDAP-related RFCs, which are numerous and varied. As a group, they tend to convey an impression of great complexity, which is somewhat unrepresentative of average age. Table 19.3 list of the high points.

# Table 19.3 Important LDAP-related RFCs

| RFC | Title |
| --- | --- |
| 2307 | An Approach for Using LDAP as a Network Information Service |
| 2820 | Access Control Requirements for LDAP |
| 2849 | LDAP Data Interchange Format (LDIF)—Technical Specification |
| 3112 | LDAP Authentication Password Schema |
| 3672 | Subentries in the Lightweight Directory Access Protocol (LDAP) |
| 4511 | LDAP: The Protocol |
| 4512 | LDAP: Directory Information Models |
| 4513 | LDAP: Authentication Methods and Security Considerations |
| 4514 | LDAP: String Representation of Distinguished Names |
| 4515 | LDAP: String Representation of Search Filters |
| 4516 | LDAP: Uniform Resource Locator |
| 4517 | LDAP: Syntaxes and Matching Rules |
| 4519 | LDAP: Schema for User Applications |

# OpenLDAP: the traditional open source LDAP server

OpenLDAP is an extension of work originally done at the University of Michigan; it continues as an open source project. It is shipped with many Linux distributions, though it is not necessarily included in the default installation. You'll need to download and install the software to run on Solaris, HP-UX, or AIX. The documentation is perhaps described as "brisk."

In the OpenLDAP distribution, slapd is the standard LDAP server daemon. In an environment with multiple OpenLDAP servers, slurpd runs on the master server and handles replication by pushing changes to slave servers. A selection of command-line tools enable the querying and modification of LDAP data.

Setup is straightforward. First, create an /etc/openldap/slapd.conf file by copying the sample installed with the OpenLDAP server.

![](bbox=[0.953, 0.183, 0.996, 0.296])