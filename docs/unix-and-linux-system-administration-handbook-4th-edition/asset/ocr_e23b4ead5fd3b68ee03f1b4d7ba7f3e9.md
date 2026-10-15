will probably have only a hub node and leaf nodes and thus will need only two versions of the conf file. A larger site may need separate hubs for incoming and outgoing mail and, perhaps, a separate POP/IMAP server.

Whatever the complexity of your site and whatever face it shows to the outside world (exposed, behind a firewall, or on a virtual private network, for example), it’s likely that the cf directory contains some appropriate ready-made configuration snippets just waiting to be customized and put to work.

# 20.10 SENDMAIL CONFIGURATION PRIMITIVES

sendmail configuration commands are case sensitive. By convention, the names of predefined macros are all caps (e.g., OSTYPE), m4 commands are all lower case (e.g., define), and configurable option names usually start with lowercase conf and end with an all-caps variable name (e.g., confBACKUP_MX). Macros usually refer to an m4 file called ../macroname/arg1.m4. For example, the reference OSTYPE(`linux') causes the file ../ostype/linux.m4 to be included.

# Tables and databases

Before we dive into specific configuration primitives, we must first discuss tables (sometimes called maps or databases), which sendmail can use to do mail routing or address rewriting. Most are used in conjunction with the FEATURE macro.

A table is a cache (usually a text file) of routing, aliasing, policy, or other information that is converted to a database format with the makemap command and then used as an information source for one or more of sendmail’s various lookup operations. Although the data usually starts as a text file, data for sendmail tables can come from DNS, NIS, LDAP, or other sources. The use of a centralized IMAP server relieves sendmail of the chore of chasing down users and obsoletes some of its tables.

Two database libraries are supported: the dbm/ndbm library that is standard with most versions of UNIX and Linux, and Berkeley DB, which is a more extensible library that supports multiple storage schemes. We recommend BDB if your system has it or you can install it. It’s faster than dbm and creates smaller files.

sendmail defines three database map types:

+   - dbm – uses an extensible hashing algorithm (dbm/ndbm)
+   - hash – uses a standard hashing scheme (DB)
+   - btree – uses a B-tree data structure (DB)

For most table applications in sendmail, the hash database type—the default—is the best. Use the makemap command to build the database file from a text file; you specify the database type and the output file base name. The text version of the database should appear on makemap’s standard input. For example:

```
$ sudo makemap hash /etc/mail/access < /etc/mail/access
```