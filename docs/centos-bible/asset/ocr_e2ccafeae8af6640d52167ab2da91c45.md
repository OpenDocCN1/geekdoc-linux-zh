# Setting Up an LDAP Address Book Server

You want to create the address book file in a format that can be loaded into the OpenLDAP database. The format you need is referred to as the **LDAP Data Interchange Format (LDIF)**. Information you enter in this format can be used to build the database and load a lot of data into the directory at once from a file.

The following steps explain how to create an LDIF file containing the definitions of your address book for the example.com LDAP directory (distinguished name) and then load that file into your LDAP server.

+   1. **Create an LDIF File** — As root user, using any text editor, create a file to hold your LDAP directory entry. In my example, I used the file */etc/openldap/people.ldif*.

> **NOTE**  When you create your LDIF file, be sure to leave a blank line before each new distinguished name (dn:) line. The blank line tells *ldappadd* to start a new entry. Without the blank line, LDAP will not think that you are starting a new distinguished name. Also, remove any blank spaces before each line, making sure that all new lines begin on column 1. (A space at the beginning of a line indicates that the new line is actually part of the preceding line.)

+   2. **Define the Organization** — You need to define the directory that you will be loading into the LDAP server. For my example, I added information defining the organization as Example Organization under the distinguished name example.com (dc=example, dc=com), by adding the following information to my people.ldif file.

```
```ldif
dn:               dc=example,dc=com
objectClass:       dcObject
objectClass:       organization
dc:               example
o:                 Example Organization
```
```

+   3. **Add an Organizational Role** — I identified the role of administrator of the address book by adding the following lines to the people.ldif file.

```
```ldif
dn:               cn=Manager,dc=example,dc=com
objectClass:       organizationalRole
cn:               Manager
description:       Example Book Administrator
```
```

+   4. **Add an Organizational Unit** — Because in this example the address book basically consists of names and addresses of members of the organization, I call the organizational unit (ou) members.

```
```ldif
dn:               ou=members,dc=example,dc=com
objectClass:       top
objectClass:       organizationalUnit
ou:               members
```
```

> **NOTE**  Although in my example I am creating an address book that is at the top of my directory structure, if you are in a large company, you will want a more complex directory structure. For example, instead of having one address book at the top of your directory structure, you may create additional organizational units for countries, locations, or departments.