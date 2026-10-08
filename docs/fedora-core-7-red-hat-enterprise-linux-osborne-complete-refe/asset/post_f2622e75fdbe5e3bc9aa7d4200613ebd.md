
Next you will have to specify a password with **rootpw**. There are entries for both plain text and encrypted versions. Both are commented. Remove the comment for one. In the following example the plain text password option is used, “secret”:

```
rootpw                secret
# rootpw              {crypt}ijFYNCsNctByg
```

For an encrypted password, you can first create the encrypted version with **slappasswd**. This will generate a text encryption string for the password. Then copy the generated encrypted string to the **rootpw** entry. On GNOME you can simply cut and paste from a terminal window to the */etc/slapd.conf* file in Text Editor (Accessories). You can also redirect the encrypted string to a file and read it in later. SSHA encryption will be used by default.

```
# slappasswd
New password:
Re-enter new password:
{SSHA}0a+szaAwELk57Y8AoD5uMULSvLcCufg5
```

The **rootpw** root password entry should then look like this:

```
rootpw              {SSHA}0a+szaAwELk57Y8AoD5uMULSvLcCufg5
```

Use the password you entered at the **slappasswd** prompt to access your LDAP directory.

The configuration file also lists the schemas to be used. Schemas are included with the **include** directive.

```
include                /etc/openldap/schema/core.schema
include                /etc/openldap/schema/cosine.schema
include                /etc/openldap/schema/inetorgperson.schema
include                /etc/openldap/schema/nis.schema
```

> **NOTE** LDAP supports the Simple Authentication and Security Layer (SASL) for secure authentication with methods like MD5 and Kerberos.

# LDAP Directory Database: ldif

A record (also known as entry) in an LDAP database begins with a name, known as a *distinguishing name*, followed by a set of attributes and their values. The distinguishing name uniquely identifies the record. For example, a name could be a username and the attribute would be the user’s e-mail address, the address being the attribute’s value. Allowable attributes are determined by schemas defined in the */etc/openldap/schema* directory. This directory will hold various schema definition files, each with a **schema** extension. Some will be dependent on others, enhancing their supported classes and attributes. The basic core set of attributes are defined in the **core.schema** file. Here you will find definitions for attributes like country name and street address. Other schemas, like **inetorgperson.schema**, specify **core.schema** as a dependent schema, making its attributes available to the classes. The inetOrgPerson schema will also define its own attributes such as jpegPhoto for a person’s photograph.

# Schema Attributes and Classes

Attributes and classes are defined officially by RFC specifications that are listed with each attribute and class entry in the schema files. These are standardized definitions and should not be changed. Attributes are defined by an **attributeType** definition. Each is given a unique identifying number followed by a name by which it can be referenced. Fields include the attribute description (DESC), search features such as EQUALITY and SUBSTR, and the object identifier (SYNTAX). See the OpenLDAP administrative guide for a detailed description.

```
attributeType ( 2.5.4.9 NAME ( 'street' 'streetAddress' )
DESC 'RFC2256: street address of this object'
EQUALITY caseIgnoreMatch
SUBSTR caseIgnoreSubstringsMatch
SYNTAX 1.3.6.1.4.1.1466.115.121.1.15{128} )
```

A class defines the kind of database (directory) you can create. This will specify the kinds of attributes you can include in your records. Classes can be dependent, where one class becomes an extension of another. The class most often used for LDAP databases is **inetOrgPerson**, defined in the **inetOrgPerson.schema** file. The term inetOrgPerson stands for Internet Organization Person, as many LDAP directories perform Internet tasks. The class is derived from the organizationalPerson class defined in **core.schema**, which includes the original attributes for commonly used fields like street address and name.

```
# inetOrgPerson
# The inetOrgPerson represents people who are associated with an
# organization in some way. It is a structural class and is derived
# from the organizationalPerson which is defined in X.521 [X521].
objectClass ( 2.16.840.1.113730.3.2.2
NAME 'inetOrgPerson'
DESC 'RFC2798: Internet Organizational Person'
SUP organizationalPerson
STRUCTURAL
MAY ( audio $ businessCategory $ carLicense $ departmentNumber $
    displayName $ employeeNumber $ employeeType $ givenName $
    homePhone $ homePostalAddress $ initials $ jpegPhoto $
    labeledURI $ mail $ manager $ mobile $ o $ pager $
    photo $ roomNumber $ secretary $ uid $ userCertificate $
    x500UniqueIdentifier $ preferredLanguage $
    userSMIMECertificate $ userPKCS12 ) )
```

You can create your own classes, building on the standard ones already defined. You can also create your own attributes. But each attribute will require a unique object identifier (OID).

# Distinguishing Names

Data in an LDAP directory are organized hierarchically, from general categories to specific data. An LDAP directory could be organized starting with countries, narrowing to states, then organizations and their subunits, and finally individuals. Commonly, LDAP directories are organized along the lines of Internet domains. In this format, the top category would be the domain name extension, for instance .com or .ca. The directory would then break down to the network (organization), units, and finally users.

This organization is used to help define distinguishing names that will identify the LDAP records. In a network-based organization, the top-level organization is defined by a domain component specified by the dcObject class, which includes the domainComponent (dc) attribute. Usually you define the network and extension as domain components to make up the top-level organization that becomes the distinguishing name for the database itself.

```
dc=mytrek, dc=com
```

Under the organization name is an organizational unit, such as users. These are defined as an organizationalUnitName (ou), which is part of the organizationalUnit class. The distinguishing name for the user's organizational unit would be

```
ou=users, dc=mytrek, dc=com
```

Under the organizational unit you could then have individual users. Here the user name is defined with the commonName (cn) attribute, which is used in various classes, including Person, which is part of organizationalPerson, which in turn is part of inetOrgPerson. The distinguishing name for the user dylan would then be

```
cn=dylan,ou=users,dc=mytrek,dc=com
```

# LDIF Entries

Database entries are placed in an LDAP Interchange Format (LDIF) file. This format provides a global standard that allows a database to be accessed by any LDAP-compliant client. An LDIF file is a simple text file with an .ldif extension, placed in the /etc/openldap directory. The entries for an LDIF record consist of a distinguishing name or attribute, followed by a colon, and its list of values. Each record begins with a distinguishing name to uniquely identify the record. Attributes then follow. You can think of the name as a record and the attributes as fields in that record. You end the record with an empty line.

Initially you create an LDIF file using any text editor. Then enter the records. In the following example, the mytrek.ldif LDIF file contains records for users on the network.

First you create records defining your organization and organization units. These distinguishing names will be used in user-level records. You will also have to specify a manager for the database, in this case simply Manager. Be sure to include the appropriate object classes. The organization uses both the dcObject (domain component object) and organization objects. The Manager uses organizationalRole, and users use the organizationalUnit. Within each record you can have attribute definitions, like the organization attribute, o, in the first record, which is set to MyTrek.

```
dn: dc=mytrek,dc=com
objectclass: dcobject
objectclass: organization
dc: mytrek
o: MyTrek

dn: cn=Manager,dc=mytrek,dc=com
cn: Manager
objectclass: organizationalRole
```
