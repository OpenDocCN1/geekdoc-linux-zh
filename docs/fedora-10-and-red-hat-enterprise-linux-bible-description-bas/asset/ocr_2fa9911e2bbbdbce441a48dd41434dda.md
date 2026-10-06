# Part IV: Fedora and RHEL Network and Server Setup

5. Save slapd.conf. Save your changes to the slapd.conf file and close it.

6. Check slapd.conf. You can check for syntax errors in your slapd.conf file by running the slaptest command, as follows:

```
- slaptest -u
config file testing succeeded
```

If something was wrong with the syntax of the file (for example, if you left off a quote or misplaced a comma), the message would say slapd: bad configuration file! Try to correct the problem and check the file again. Later, when the databases are created, you can run slaptest again (without the -u option) to make sure slapd.conf points to exists, properly configured databases.

At this point, you can try starting the OpenLDAP service

# Starting the OpenLDAP service

You start OpenLDAP as you do most services in Fedora and RHEL systems, using the service and chkconfig commands. The service name for OpenLDAP is ldap. To start the service immediately, type the following:

```
# service ldap start
Starting slapd:                               [ OK ]
```

To set the ldap service to start each time the system is rebooted, type the following:

```
# chkconfig ldap on
```

By default, the ldap service will read permissions open to everyone.

# Setting Up the Address Book

When I set up the structure of the address book database, I base the distinguished name (dn) for the database on the organization's name (in this example, linuxuxoys).

With the suffix set to linuxuxoys.net (suffix "dc=linuxuxoys,dc=net") in the slapd.conf file (which yours will be different), the backend database is set up to handle queries to the distinguished name (dn) linuxuxoys.net. You can create the structure for the address book for that distinguished name.

> NOTE: The dc stands for Domain Component. When you include a domain name as your distinguished name, in the order which you put the parts of that domain name place the part closest to the DNS root last. In this example, the dc=linuxuxoys comes before dc=net. See RFC 2247 if you are interested in the specification for including domain names in LDAP directories.

You want to create the address book file in a format that can be loaded into the OpenLDAP database. The format you need is referred to as LDAP Data Interchange Format (LDIF).