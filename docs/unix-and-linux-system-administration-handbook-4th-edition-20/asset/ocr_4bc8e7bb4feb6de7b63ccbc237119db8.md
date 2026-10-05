# 19.3 LDAP: THE LIGHTWEIGHT DIRECTORY ACCESS PROTOCOL

UNIX Linux sites need a good way to distribute their administrative configuration data; however, the problem is really more general than that. What about nonadministrative data such as telephone and email directories? What about information you want to share with the outside world? What everyone really needs is a generalized directory service.

A directory service is just a database, but one that makes a few assumptions. Any data set that has characteristics matching the assumptions is a candidate for inclusion in the directory. The basic assumptions are as follows:

+   * Data objects are relatively small.
* The database will be widely replicated and cached.
* The information is attribute based.
* Data are read often but written infrequently.
* Searching is a common operation.

The current IETF standards-track system designed to fill this role is the Lightweight Directory Access Protocol (LDAP). The LDAP specifications don't really speak to the database itself, just the way it's accessed through a network. But because they specify how the data is schematized and how searches are performed, they imply a specific data model as well.

LDAP was originally designed as a gateway protocol that would allow TCP/IP clients to talk to an older directory service called X.500, which is now obsolete. Over time, it became apparent that X.500 was dying to out and that UNIX really needed a standard of some sort. These factors have led to LDAP being developed as a full-fledged directory in its own right (and perhaps to its no longer being so quaint as the of L).

At this point, LDAP has become mainstream, spurred perhaps by Microsoft's adoption of LDAP as the basis for its Active Directory service. On UNIX and Linux side, the OpenLDAP package (openldap) has become the standard implementation. The 389 Directory Server (formerly Directory Directory and Netscape Directory Server) is also open source and can be found at port389.org. It runs on Linux, Solaris, and HP-UX.

# The structure of LDAP data

LDAP takes the form of property lists, which are known in LDAP world as "entries.\ Each entry consists of a set of attributes (such as description or uid) along with those attributes' values. Windows users might recognize this structure as being similar to that of the Windows registry. As in the registry, an individual attribute can have several values.

4. Because of LDAP's tortured history, many sources tend to go into great detail about LDAP's X.500 and OSI connections. However, this history is not relevant to contemporary use of LDAP. Ignore it.