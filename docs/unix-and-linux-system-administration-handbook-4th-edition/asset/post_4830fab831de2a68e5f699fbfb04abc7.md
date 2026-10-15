
## The point of LDAP

Until you’ve had some experience with it, LDAP can be a slippery concept to grab hold of. LDAP by itself doesn’t solve any specific administrative problem. There’s no “primary task” that LDAP is tailor-made to handle, and sites diverge widely in their reasons for deploying LDAP servers. So before we move on to the specifics of installing and configuring OpenLDAP, it’s probably worth reviewing some reasons why you might want to investigate LDAP for use at your site.

Here are the big ones:

- LDAP can act as a central repository for information about your users, including everything from their phone numbers and home addresses to their login names and passwords.
- In a similar vein, you can use LDAP to distribute configuration information for ancillary applications. Most mail systems—including sendmail, Exim, and Postfix—can draw a large part of their routing information from LDAP, and this is in fact one of LDAP’s most popular applications. Tools as varied as the Apache web server and the autofs automounter can be configured to pay attention to LDAP, too. It’s likely that LDAP support will become more and more common over time.
- LDAP makes it easy for applications (even those written by other teams and other departments) to authenticate users without having to worry about the exact details of account management.
- Changes to LDAP data take effect immediately and are instantly visible to all hosts and client applications.
- It’s easy to access LDAP data through command-line tools such as ldapsearch. In addition, LDAP is well supported by common scripting languages such as Perl and Python (through the use of libraries). Ergo, LDAP is a terrific way to distribute configuration information for locally written scripts and administrative utilities.
- Excellent web-based tools are available for managing LDAP, some examples being phpLDAPadmin (phpldapadmin.sourceforge.net) and Directory Administrator (diradmin.open-it.org). These tools are so easy to use that you can just rip the box open and start playing without reading the manual.

See page 774 for more information about using LDAP with sendmail.

UNIX," and now "Windows Server 2008 UNIX Interoperability Components") that facilitate the mapping of UNIX users and groups. See Chapter 30, Cooperating with Windows, for more information about integrating your UNIX systems with Active Directory-based LDAP.

## LDAP documentation and specifications

A good general introduction to LDAP is LDAP for Rocket Scientists, which covers LDAP architecture and protocol. Find it on-line at zytrax.com/books/ldap. Another good source of information is the LDAP-related RFCs, which are numerous and varied. As a group, they tend to convey an impression of great complexity, which is somewhat unrepresentative of average use. Table 19.3 lists some of the high points.

### Table 19.3 Important LDAP-related RFCs

| RFC | Title |
|---|---|
| 2307 | An Approach for Using LDAP as a Network Information Service |
| 2820 | Access Control Requirements for LDAP |
| 2849 | LDAP Data Interchange Format (LDIF)—Technical Specification |
| 3112 | LDAP Authentication Password Schema |
| 3672 | Subentries in the Lightweight Directory Access Protocol (LDAP) |
| 4511 | LDAP: The Protocol |
| 4512 | LDAP: Directory Information Models |
| 4513 | LDAP: Authentication Methods and Security Mechanisms |
| 4514 | LDAP: String Representation of Distinguished Names |
| 4515 | LDAP: String Representation of Search Filters |
| 4516 | LDAP: Uniform Resource Locator |
| 4517 | LDAP: Syntaxes and Matching Rules |
| 4519 | LDAP: Schema for User Applications |

## OpenLDAP: the traditional open source LDAP server

OpenLDAP is an extension of work originally done at the University of Michigan; it now continues as an open source project. It's shipped with most Linux distributions, though it is not necessarily included in the default installation. You'll need to download and install the software to run it on Solaris, HP-UX, or AIX. The documentation is perhaps best described as "brisk."

In the OpenLDAP distribution, slapd is the standard LDAP server daemon. In an environment with multiple OpenLDAP servers, slurpd runs on the master server and handles replication by pushing changes out to slave servers. A selection of command-line tools enable the querying and modification of LDAP data.

Setup is straightforward. First, create an /etc/openldap/slapd.conf file by copying the sample installed with the OpenLDAP server.
