# SETTING UP AN LDAP SERVER

gufw (page 876), open one of these ports by adding a rule that allows service for port
389 or port 636 from the clients you want to be able to access the server.

# SET UP THE SERVER

Back end OpenLDAP uses the Directory Information Tree (DIT) hierarchy with its root at
/etc/ldap/slapd.d/cn=config (the equal sign is part of the directory name) to configur-
re slapd daemon. This setup allows for dynamically (without having to restart the daemon). You must configure this DIT, referred
as the back end, before you can add user data to the LDAP database.

Front end The end of the database also needs to be configured before you can add user\data You must use it to hold the data of the user wants to store. “Set Up
The Front End” on page 762 describes how to set up a database that is compatible
with many address applications.

Once you have set up the back end and the front end, you can add user data as
in in the section “Add Entries to the Directory” on page 764.

This section lists the steps involved in setting up an LDAP server at sobell.com
domain. When you set up an LDAP server, substitute the name of the server
you are setting up for sobell.com in the examples.

To experiment and learn about LDAP, set up and run locally the example server
described in this section. Although the example uses sobell.com, when working from
the server system you can refer to the LDAP server as localhost.

# SET UP THE BACK END

You need to add three files and one setup file to the back end before you can
add information to the front end of the LDAP database. Installing LDAP installs the
three files. Use the following commands to add these files to the LDAP
directory:

```
$ sudo ldapadd -Y EXTERNAL -H ld:/// -f /etc/ldap/schema/cosine.ldif
SASL/EXTERNAL authentication started
SASL username: uidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
adding new entry "cn=cosine,cn=schema,cn=config"
```

```
$ sudo ldapadd -Y EXTERNAL -H ld:/// -f /etc/ldap/schema/nis.ldif
$ sudo ldapadd -Y EXTERNAL -H ld:/// -f /etc/ldap/schema/inetorgperson.ldif
```

The following files set up the back end of the LDAP database with a DSE compris-
ing DC sobell and the DC com (page 758) and an administrative user named
admin with a password of popcupine. Change these values as is appropriate for the
database you are setting up. (Note the fourth line from the bottom is long and is
wrapped in the following display. This file is available on the Web at
www.sobell.com/UB3/code/chapter_21/backend.setup.ldif.)