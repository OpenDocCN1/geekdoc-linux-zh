
for the password (-w). The only difference is the -f parameter to specify the location of the LDIF file we have created. All being well, the entries in the LDIF file will be added to the LDAP server.

Now that you have the organizational structure in the LDAP server, you need to populate it with some objects.

## Adding User Data to the LDAP Server

You need to define what information you hold about users before you create the LDIF files. As you are going to use this information to hold user accounts as well as information about users, you will use the inetOrgPerson, person, posixAccount, shadowAccount, and organizationalPerson object classes.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_689_0.png)

You can find more information about the data you can use in an LDIF file and also in an LDAP server in the OpenLDAP schemas. These are located in /etc/openldap/schema.

Referring to the schema in /etc/openldap/schema, you can see that the person object class can contain the information shown in Table 25-1.

## Table 25-1
person Object Class

| Element | Description |
|---|---|
| sn | Second name* |
| cn | Common name* |
| UserPassword | Password |
| Telephone | Contact number |
| SeeAlso | Freeform referral entry |
| Description | Description of the user |

*Must be in the object class

Each object class defines what each object can contain, and this information is defined in the LDAP schema files. For more information on what is included in an object class, view the schema files in /etc/openldap/schema.

You now need to construct an LDIF file for the users. In Listing 25-4, we detail one of the users so that you can see how her profile would look in this organization.

## Listing 25-4: LDIF Listing for Aimee Davies

```
dn: aimee,ou=Administrators,ou=IT,o=Acme,c=UK
uid: aimee
cn: Aimee Davies
givenName: Aimee
sn: Davies
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: top
objectClass: shadowAccount
userPassword: [crypt]ESlp8fJpWVEE
shadowLastChange: 12572
shadowMax: 99999
shadowWarning: 7
loginShell:/bin/bash
uidNumber: 1000
gidNumber: 100
homeDirectory:/home/aimee
telephoneNumber: 555-1027
o: UK
gecos: Aimee Davies
```

We have constructed an LDIF file for the administrator Aimee Davies, including account information allowing her to use the LDAP data as a Unix authentication source.

To construct the initial LDIF file, we used the PWED migration tools to transfer a standard user account from /etc/passwd to an LDIF format file, editing this file to add the extra information about the organization and her telephone number.

You can add each user in the organization to the specific organization unit that reflects the organizational chart. Using the ldapsearch command, you can now view the data in the LDAP server (see Listing 25-5). You use the -b option to tell ldapsearch to search from o=Acme,c=UK base of the LDAP tree. This enables you to search a certain portion of the LDAP tree, not the whole tree.

## Listing 25-5: Output of ldapsearch for the Entire LDAP Database

```
/etc/ldap/schema ldapsearch -x -b "o=Acme,c=UK"
# extended LDIF
# LDAPv3
# base=<o=Acme,c=UK> with scope sub
```

## Working with LDAP in SUSE

```
# filter: (objectClass=*)
# requesting: ALL
# Acme, UK
dn: o=Acme,c=UK
o: Acme
objectClass: top
objectClass: organizational

# Sales, Acme, UK
dn: ou=Sales,o=Acme,c=UK
ou: Sales
objectClass: top
objectClass: organizationalUnit

# Marketing, Acme, UK
dn: ou=Marketing,o=Acme,c=UK
ou: Marketing
objectClass: top
objectClass: organizationalUnit

# IT, Acme, UK
dn: ou=IT,o=Acme,c=UK
ou: IT
objectClass: top
objectClass: organizationalUnit

# HR, Acme, UK
dn: ou=HR,o=Acme,c=UK
ou: HR
objectClass: top
objectClass: organizationalUnit

# Services, Acme, UK
dn: ou=Services,o=Acme,c=UK
ou: Services
objectClass: top
objectClass: organizationalUnit

# Helpdesk, IT, UK
dn: ou=Helpdesk,ou=IT,o=Acme,c=UK
ou: Helpdesk
objectClass: top
objectClass: organizationalUnit

# Architects, IT, UK
dn: ou=Architects,ou=IT,o=Acme,c=UK
ou: Architects
objectClass: top
objectClass: organizationalUnit
```

## Listing 25-5: (continued)

```
# Administrators, IT, UK
dn: ou=Administrators,ou=IT,o=Acme,c=UK
ou: Administrators
objectClass: top
objectClass: organizationalUnit

# aime, Administrators, IT, UK
dn: uid=aime,ou=Administrators,ou=IT,o=Acme,c=UK
uid: aime
cn: Aimee Davies
givenName: Aimee
sn: Davies
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: top
objectClass: shadowAccount
userPassword: [crypt]ESlp8fJpWVEE
shadowLastChange: 12572
shadowMax: 99999
shadowWarning: 7
loginShell:/bin/bash
uidNumber: 1000
gidNumber: 100
homeDirectory:/home/aimee
telephoneNumber: 555-1027
o: UK
gecos: Aimee Davies

# search result
search: 2
result: 0

# numResponses: 11
numEntries: 10
```

The initial population of the LDAP server with the organization structure and the addition of Aimee Davies is reflected in Listing 25-5.

If you want to see Aimee's telephone number, use the ldapsearch command to filter the output (see Listing 25-6).

## Listing 25-6: Searching for a Specific User and Filtering

```
/etc/ldap/schema ldapsearch -x -b=Acme,c=UK "uid=aime"
# extended LDIF
# LDAPv3
# base=<o=Acme,c=UK> with scope sub
# filter: uid=aime
# requesting: telephoneNumber
# aime, Administrators, IT, Acme UK
dn: uid=aime,ou=Administrators,ou=IT,o=Acme,c=UK
telephoneNumber: 555-1027

# search result
search: 2
result: 0

# numResponses: 2
numEntries: 1
```

In the previous listing, we used the standard ldapsearch parameters, added a term to search for (in quotes), and also the object data we want to view.

The term to search should be unique to a user account; otherwise you will receive multiple entries. In the case of the organization, we know that the UID of a person is unique, as it must be when used as a username in Unix. If you want to search specifically for an entry, you can explicitly search for the whole of the DN for the user.

## Pluggable Authentication Modules

Before Pluggable Authentication Modules (PAM) came along, any application that needed to authenticate a user had to read the /etc/passwd and /etc/shadow files directly. This restricted how data was stored because the data always had to be in a text file.

PAM provides authentication modules that can obtain user accounts from numerous sources, an LDAP server, a SQL database, or a Windows Active directory, for example.

PAM works by having a configuration file for each service that needs to authenticate users. For example, the login process has a separate PAM configuration file, as does the imap service.

These service configuration files are stored in /etc/pam.d and contain information about how the process gets information about the user, their account data, and passwords. Each file can contain four types of entries, discussed in Table 25-2.

## Table 25-2
PAM Configuration Entries

| Entry | Description |
|---|---|
| account | Used to check whether the user is allowed to log in, what the account expiry is, and so on. |
| password | Used to change the user's password. |
| auth | Used to check the user's password. |
| session | Used to enable or disable features of the user's session after he or has authenticated. This can be used to mount the user's home directory automatically. |

> Note
PAM is not just for usernames and passwords; it is a general authentication library and can be used to check a smart card owned by the user to authenticate or in the future to read biometric data from the user, such as facial recognition.

For each entry type, you can specify a PAM module to handle the account, password-authentication, or session data related to a user account.

For example, if you want to allow the imap service to authenticate data to the system /etc/passwd and /etc/shadow, you need at minimum an account and authentication entry. This enables a user to log in if his or her account is active and also check whether the password provided by the user is correct.

```
auth required /lib/security/pam-unix.so nullok
account required /lib/security/pam-unix.so
```

This file has a bit of information in it, and you can see an entry for auth and account. The second, third, and fourth fields are also very important when configuring PAM for your service.

The second field determines how the data received back from the PAM module (specified in field three) is acted upon. When a PAM module is used, it returns
