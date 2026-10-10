
1. **Create an ldif file.** As root user, using any text editor, create a file to hold your LDAP directory entry. In my example, I used the file /etc/openldap/toypeople.ldif.

> **NOTE:** When you create your ldif file, be sure to leave a blank line before each new distinguished name (dn:) line. The blank line tells ldapadd to start a new entry. Without the blank line, LDAP will not think that you are starting a new distinguished name. Also, remove any blank spaces before each line, making sure that all new lines begin on column 1. (A space at the beginning of a line indicates that the new line is actually part of the preceding line.)

2. **Define the organization.** You need to define the directory that you will be loading into the LDAP server. For my example, I added information defining the organization as Linux Toys under the distinguished name linuxtoys.net (dc=linuxtoys,dc=net), by adding the following information to my toypeople.ldif file.

```
dn:    dc=linuxtoys,dc=net
objectClass:  dcObject
objectClass:  organization
dc:           linuxtoys
o:           Linux Toys
```

3. **Add an organizational role.** I identified the role of administrator of the address book by adding the following lines to the toypeople.ldif file.

```
dn:           cn=Manager,dc=linuxtoys,dc=net
objectClass: organizationalRole
cn:           Manager
description: LinuxToys Address Book Administrator
```

4. **Add an organizational unit.** Because in this example the address book basically consists of names and addresses of members of the organization, I call the organizational unit (ou) members.

```
dn:           ou=members,dc=linuxtoys,dc=net
objectClass:  top
objectClass:  organizationalUnit
ou:          members
```

> **NOTE:** Although in my example I am creating an address book that is at the top of my directory structure, if you are in a large company chances are that you will want a more complex directory structure. For example, instead of having one address book at the top of your directory structure, you may create additional organizational units for countries, locations, or departments. Then, every single unit might have its own address book. You also might want to support multiple directories under each unit. For example, there may be a separate directory for keeping track of computer equipment or company vehicles.

5. **Add people.** With the directory structure in place, and with a members unit under the linuxtoys.net distinguished name, I can begin adding people to the directory. I define each person as organizationalPerson and inetOrgPerson object classes. There are a lot of different attributes I could add to each person's information. However, most of the attributes I've chosen are attributes that will be read by the Thunderbird mail client (which I will show later in this chapter). Here are the two entries:

```text
dn: cn=John Jones,dc=linuxtoys,dc=net
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: John Jones
mail: jwJones@linuxtoys.net
givenname: John
sn: Jones
uid: jwJones
o: Linux Toys
telephoneNumber: 800-555-1212
homePhone: 800-555-1313
mobile: 800-555-1414
pager: 800-555-1515
facsimileTelephoneNumber: 800-555-1414
title: Account Executive
homePostalAddress: 1515 Broadway$New York NY 99999
```

```text
dn: cn=Sheree Glass,dc=linuxtoys,dc=net
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: Sheree Glass
mail: sheree@linuxtoys.net
givenname: Sheree
sn: Glass
uid: slglass
o: Linux Toys
telephoneNumber: 800-555-2893
homePhone: 800-555-4329
mobile: 800-555-8458
pager: 800-555-4955
facsimileTelephoneNumber: 800-555-3838
title: Interior Decorator
homePostalAddress: 167 E Street$Salt Lake UT 99999
```

As you can see here, the two people listed in the address book directory (called `members`) are each associated with a common name (cn), John Jones and Sheree Glass, which falls under the linuxtoys.net domain components. You can add as many people as you want to this file by repeating this structure. (Notice that a `$` is used to separate lines in an address.)

> **NOTE:** You may find that you don't need all of the attributes shown here or may want to add others. Refer to the schema files to see a list of attributes that are available with `organizationalPerson`, `inetOrgPerson`, and other object classes you might want to use with your address book.

6. **Save the ldif file**. Save the changes to your ldif file (in my case, the file is called `/etc/openldap/toypeople.ldif`).

7. **Add the information to the LDAP server**. You can use the `ldapadd` command to add the entire contents of the ldif file you created to your LDAP directory. Here is the command I used to add the contents of my ldif file (called `toypeople.ldif`) to my LDAP directory:

```
# ldapadd -xv -D "cn=Manager,dc=linuxtoys,dc=net" -W -f toypeople.ldif
Enter LDAP Password: mysecret
adding new entry "dc=linuxtoys,dc=net"

adding new entry "cn=manager,dc=linuxtoys,dc=net"
adding new entry "ou=members,dc=linuxtoys,dc=net"
adding new entry "cn=John Jones,dc=linuxtoys,dc=net"
adding new entry "cn=Sheree Glass,dc=linuxtoys,dc=net"
```

The password shown here (which will not display as you type it) is the one you added to your `slapd.conf` file. In the example, I used `mysecret` as the password. The -x says to use simple authentication (no SASL). The -D says to use the distinguished name defined earlier in the `slapd.conf` file (`cn=Manager,dc=linuxtoys,dc=net`). The -W says to prompt for the password, instead of entering it on the command line. The -f indicates the file to load (in the example presented here, `toypeople.ldif`).

As the `ldapadd` command successfully adds each entry, it lists the distinguished name (`dn`) associated with each one.

8. **Restart the server**. You can restart the server at this point by typing the following:

```
# /etc/init.d/ldap restart
```

9. **Search the directory**. To make sure that everything was properly inserted into the directory, you can run the following search command:

```
# ldapsearch -x -D 'cn=manager,dc=linuxtoys,dc=net' \
#  -b 'dc=linuxtoys,dc=net' ' (objectClass=* ) '

# extended LDIF
#
# LDIFv3
# base <dc=linuxtoys,dc=net> with scope subtree
# filter: (objectClass=*)
# requesting: ALL
#
#
# linuxtoys.net
dn: dc=linuxtoys,dc=net
objectClass: top
objectClass: dcObject
objectClass: organization
dc: linuxtoys
o: Linux Toys

# Manager, linuxtoys.net
dn: cn=Manager,dc=linuxtoys,dc=net
objectClass: organizationalRole
cn: Manager
description: LinuxToys Address Book Administrator

# members, linuxtoys.net
dn: ou=members,dc=linuxtoys,dc=net
objectClass: top
objectClass: organizationalUnit
ou: members

# John Jones, linuxtoys.net
dn: cn=John Jones,ou=members,dc=linuxtoys,dc=net
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: John Jones
mail: jjones@linuxtoys.net
givenName: John
sn: Jones
uid: jjones
o: Linux Toys
.
.

# Sheree Glass, linuxtoys.net
dn: cn=Sheree Glass,ou=members,dc=linuxtoys,dc=net
objectClass: top
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: Sheree Glass
mail: sheree@linuxtoys.net
.
.
```

In this example, I asked to use simple authentication (clear-text passwords with the -x option), start at the base (-b) of the linuxtoys.net directory to begin the search, and list all object classes (objectClass=*). If you like, you can pipe the output to less so you can page through it.

10. **Debug your directory.** Don't expect your ldif file to load the first time without any errors. While you debug your address book directory, I recommend that you use a non-production machine and just clear out the database files after each failed attempt to load your directory. Assuming that you kept your LDAP directory files in `/var/lib/ldap` and that it's okay to erase the whole database while you debug your entries, you can do the following:

> CAUTION: You're about to erase the LDAP directory files you created. Don't do this step if you have information in your LDAP directory files that is not in your ldif file. Don't erase your ldif file because you need it to recreate your directory files.

```bash
# /etc/init.d/ldap stop
# rm /var/lib/ldap/*
# /etc/init.d/ldap restart
# ldapadd -x -D "cn=Manager,dc=linuxtoys,dc=net" -W -f toypeople.ldif
```

Repeat this process until you feel that your ldif file, and all the information it contains, has been properly loaded into your LDAP directory files.

At this point, you can decide if you need to further tune your LDAP directory (as described in the section “More ways to configure LDAP”). After that, I recommend that you check that your LDAP address book directory is working properly by trying to access it from Thunderbird, using its Contacts feature (as described later in this chapter).

## More Ways to Configure LDAP

If you plan to scale up your LDAP directory to be used by more than just a small office or home e-mail server, there are some additional configuration options you might want to consider. Here are a few suggestions:

- Replicate the LDAP directory — You can make your LDAP directory accessible from multiple LDAP servers and have updates to your directory be disseminated to those servers. See the man page for the slurpd daemon (which handles update replication) and the OpenLDAP Administrator’s Guide for information on setting up LDAP directory replication (`/usr/share/doc/openldap-servers/guide.html`).
- Add certificates — Transport Layer Security is built into the OpenLDAP server. For information on defining certificates and ciphers that will be accepted by the slapd daemon, refer to the slapd.conf man page.
- Change log levels — You can specify the level of debugging that is done by the slapd daemon. By adding the loglevel `<integer>` option to the slapd.conf file, you can have slapd do the following types of logging:
    - 1   Trace function calls
    - 2   Debug packet handling
    - 4   Heavy trace debugging
    - 8   Connection management
