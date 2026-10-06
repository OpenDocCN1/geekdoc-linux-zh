
# Chapter 22: Setting Up an LDAP Address Book Server 899

Information you enter in this format can be used to build the database and load a lot of data into the directory at once from a file.

The following steps explain how to create an LDIF file containing the definitions of your address book for the linuxtoys LDAP directory (distinguished name), and then load that into your LDAP server:

- 1. Create an ldif file. As root user, using any text editor, create a file to hold your LDAP directory entry. In my example, I used the /etc/openldap/toypeople.ldif.

> NOTE: When you create your ldif file, be sure to leave a blank line before each distinguished name (dn:). The blank line tells LDAP to start a new entry. Without the blank line, LDAP will not think that you are starting a new distinguished name. Also, remove any blank spaces before each line, making sure that new lines begin on column 1. (A space at the beginning of a line indicates that the new line is actually part of the preceding line.)

- 2. Define the organization. You need to define the directory that will be loading into the LDAP server. For my example, I added information defining the organization as Linux Toys under the distinguished name linuxtoys.dc=linuxtoys,dc=net, by adding the following information to my toypeople.ldif file.

```
dn=linuxtoys,dc=net
objectClass=object
objectClass=organization
dc=linuxtoys
ou=Linux Toys
```

- 3. Add an organizational role. I identified the role of administrator of the address book by adding the following lines to the toypeople.ldif file.

```
dn=Manager,dc=linuxtoys,dc=net
objectClass=organizationalRole
cn=Manager
description=LinuxToys Address Book Administrator
```

- 4. Add an organizational unit. Because in this example the address book basically consists of names and addresses of members of the organization, I call the organizational unit (ou) members.

```
dn=ou=members,dc=linuxtoys,dc=net
objectClass=top
objectClass=organizationalUnit
ou=members
```

NOTE: Although in my example I am creating an address book that is at the top of my directory structure, if you are in a large company chances that you will want a more complex structure. For example, instead of having one address book at top of your directory, you may create additional organizational units for countries, or departments. Then every single unit might have its own address book. You may also want to support multiple directories under each unit. For example, there may be a separate directory for keeping track of computer equipment or vehicles.

- 5. Add people. With the directory structure in place, and with members unit under linux.net, I can begin adding people to the directory. I define each person as organizationalPerson and orgPerson classes. However, there are a lot of different attributes I could add to each person. Most of the attributes I've chosen will be read by the Thunderbird client (which I will show later). Here are two entries:

```
dn=cn=John Jones,dc=linuxtoys,dc=net
objectClass=organizationalPerson
objectClass=orgPerson
cn=John
mail=jwones@linuxtoys
givenName=John
sn=Jones
uid=jjones
o=Linux Toys
```

```
dn=cn=Shree Glass,dc=linuxtoys,dc=net
objectClass=organizationalPerson
objectClass=orgPerson
cn=Shree
mail=sheree@linuxtoys
givenName=Shree
sn=Glass
uid=sglass
o=Linux Toys
```

# Chapter 22: Setting Up an LDAP Address Server 901

As you can see here, the two people listed in the address book directory (called members) are each associated with a common name (cn), John Jones and Shree Glass, which falls under the linuxtoys.net domain components. You can add as many people as you want to this file by repeating this structure. Notice that , is used to separate lines.

> NOTE: You may find that you don't need all of the attributes shown here or may want to add others. Refer to the schema files to see a list of attributes that are available with organizationalPerson, inetOrgPerson, and other classes you might want to use with your address book.

- 6. Save the ldif. Verify the changes to your ldif (in my case, the file is called /etc/ldap/toypeople.ldif).

- 7. Add the information to the LDAP server. You can use the ldapadd command to add the entire contents of the ldif you created to your LDAP directory. Here is the command I used to add the contents of my ldif file (called toypeople.ldif) to my LDAP directory.

```
# ldapadd -xv -D "cn=Manager,dc=linuxtoys,dc=net" -W -f toypeople.ldif
LDAP Password: mysecret
add objectClass:
  dcObject
  organization
add dc:
  linuxtoys
  Linux Toys
adding new entry "dc=linuxtoys,dc=net"
modify complete
add objectClass:
  organizationalRole
add cn:
  Manager
add description:
  Linuxtoys Address Book Administrator
adding new entry "cn=Manager,dc=linuxtoys,dc=net"
modify complete
add cn:
  John Jones
add mail:
  jwjones@linuxtoys.net
add givenname:
  John
add sn:
  Jones
```

# Part IV: Fedora and RHEL Network and Server Setup

```
add cn:
  Shree Glass
add mail:
  shree@linxtoys.net
add givenname:
  Shree
add sn:
  Glass
```

The password shown here (which will not display as you type it) is the one added to the slapd.conf file. In the example, I used mysecret as the password. The -x says to use simple authentication (no SASL). The -D says to use the distinguished name defined in the slapd.conf file (cn=Manager, dc=linuxtoys, dc=net). The -f says to prompt for the password, instead of entering it in the command line.

As the ldapadd command successfully adds each entry, it lists the objects associated with each one.

- 8. Restart the server. You can restart the server at this point by typing the following:
```
# /etc/init.d/ldap restart
```

- 9. Search the directory. To make sure everything was properly inserted into the directory, you can run the following search command:

```
# ldapsearch -x -W -D 'cn=manager, dc=linuxtoys,dc=net' -b 'dc=linuxtoys,dc=net' '(objectClass=*)' -LDIF
dn=linuxtoys,dc=net
objectClass=top
objectClass=dcObject
objectClass=organization
dc=linuxtoys
o=Linux Toys
```

# Chapter 22: Setting Up an LDAP Address Server 903

```
# Manager,linuxtoys.net
dn=Manager,dc=linuxtoys,dc=net
objectClass=organizationalRole
cn=Manager
description=LinuxTools Address Book Administrator

# members,linuxtoys.net
dn=ou=members,dc=linuxtoys,dc=net
objectClass=top
objectClass=organizationalUnit
ou=members

# John Jones,linuxtoys.net
dn=cn=John Jones,ou=members,dc=linuxtoys,dc=net
objectClass=organizationalPerson
objectClass=inetOrgPerson
cn=John
mail=jwones@linuxtoys.net
givenName=John
sn=Jones
uid=jjones
o=Linux Toys

# Shree Glass,linuxtoys.net
dn=cn=Shree Glass,ou=members,dc=linuxtoys,dc=net
objectClass=organizationalPerson
objectClass=inetOrgPerson
cn=Shree
mail=sheree@linuxtoys.net
givenName=Shree
sn=Glass
uid=sglass
o=Linux Toys
```

- 10. Debug your directory. Don't forget your ifd file to load the first time without any errors. While you debug your address book directory, I recommend that you use a nonproduction machine and just clear out the database files after each failed to load your directory. Assuming that you kept your LDAP directory files in /var/lib/ldap and that it's okay to erase the whole database while you debug your entries, you can do the following:
