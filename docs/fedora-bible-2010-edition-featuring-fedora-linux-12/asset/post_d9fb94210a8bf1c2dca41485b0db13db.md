
**NOTE:** The 389 Directory Server (originally called Fedora Directory Server) was released in June 2005 as an alternative open source LDAP server to the OpenLDAP software described in this chapter. The 389 Directory Server is now part of the Fedora repository (389-ds-base and 389-ds-base-devel packages). To learn more about 389 DS, see `http://directory.fedoraproject.org`.

## Understanding LDAP

LDAP lets people create directories of information that can be shared among client applications over a network. It is particularly geared toward applications that are used to look up information that is fairly stable over and over again (in other words, information that’s being looked at more than it’s being changed). That’s why LDAP is popular for uses such as storing information about people, addresses, and other kinds of data that may require high access with relatively few changes.

Because of LDAP’s extraordinarily flexible design, as an LDAP developer or administrator you have a lot of control over:

- How the information in the directory is organized.
- How and by whom information can be accessed.
- The scale, local to global, by which information is distributed. (Information can be replicated to other servers at any scale you choose and synced up automatically.)

Despite its flexibility, however, you don’t have to begin designing each directory you create from scratch. LDAP has many predefined structures of information that you can rely on to build your LDAP directories. Those data structures are defined in several different standards documents referred to as RFCs (Request for Comments) that you can list from the IETF site (`http://www.ietf.org/rfc.html`). There are RFCs for almost every aspect of the Internet protocols and related application services. Important RFCs for LDAP definitions include:

- **RFC 2252** — Defines the framework for LDAP.
- **RFC 2256** — Defines the X.500 user schema for LDAPv3.
- **RFCs 1274, 2079, 2247, 2307, 2587, 2589** — Define specifications for including user attributes, Uniform Resource Identifiers (URIs), domain names, NIS data, public key infrastructure (PKI), and dynamic directory services in LDAP directories.

The documents on which these RFCs are based include the CCITT X.500 standard and the related ISO IS9594 directory services standards. In particular, X.521 and X.520 define some of the most basic object classes and attribute types.

Keep in mind, however, that these standards provide only guidelines. When you put together your own LDAP directory, your OpenLDAP server will have to deal directly with the schemas that implement those standards on the OpenLDAP server.

**TIP:** Microsoft’s Active Directory (AD) is often touted as an “LDAP-based” entity, giving some users high hopes of integrating OpenLDAP and AD. While it is possible to exchange information between AD and OpenLDAP, setting this up requires a lot of patience and skill. Unless you must interoperate with AD, a better path for supporting Windows clients is through the use of OpenLDAP and Samba.

## Defining information in schemas

The elements that make up LDAP directories are organized into what are called *schemas*. When you create or use an LDAP directory, the types of information in the schemas you will be working with include the following types of items:

- **Object classes** — An object provides a name under which you would group a bunch of attributes. So, with an address book, you might include the inetOrgPerson object class, under which you could store attributes associated with a person.
- **Attributes** — As its name implies, an attribute holds a piece of information associated with an object class. For example, the inetOrgPerson object class could have attributes such as telephone number, e-mail address, and so on.

**NOTE:** If you are familiar with databases, the LDAP directory terminology might seem a bit different to you. LDAP is more of a directory structure provider than a real database. You can think of attributes as fields and object classes as tables.

Examples of object classes include *country*, *locality*, and *organization*. For each object class, attributes and a list of optional attributes may be required. You can see the definitions for many standard object classes and attributes in the schema files that come with any LDAP server.

In OpenLDAP, several default schemas are included in the `/etc/openldap/schema` directory. The example e-mail address book I show you how to create in this chapter relies entirely on schemas provided with OpenLDAP. You don’t have to create any schema files yourself to do the examples in this chapter. If you need more objects and attributes than are provided by default, you can get schemas from other places or create your own.

**CROSS-REFERENCE:** For information on schemas included with OpenLDAP, refer to the OpenLDAP Schema Specification page (<http://www.openldap.org/doc/admin24/schema.html>). That page also describes how you can go about extending those schemas. Check those schemas, as well as the schema definitions in RFCs described earlier, before you create your own object classes or attributes.

As you begin dealing with your LDAP directory, you will access the object classes and attributes as names. To the LDAP server, however, each of those items is represented by a unique string of numbers and dots. Each string is referred to as an Object Identifier (OID). If you are not creating your own object classes or attributes, you don’t need to deal with OIDs.

To understand what OIDs are and when you might want to get your own OID assignment, refer to the sidebar “Understanding OIDs.”

## Structuring your LDAP directories

While standards documents are used to keep the object classes, attributes, and other elements of LDAP directories unique, you are free to put together those elements into your own LDAP directories however you want. The structure you use to create your LDAP databases is the LDAP Data Interchange Format (LDIF).

Every piece of information you store in your LDAP directory must fall under a base distinguished name (or base dn). Because many organizations these days can be represented by a unique Internet domain name, the domain name is a popular way to identify an LDAP base dn. In fact, for the examples in this chapter, the base distinguished name I use is linuxtoys.net. If you are creating an LDAP directory for an organization that can be represented by a domain name, you can replace linuxtoys.net with your domain name.

If you are creating an LDAP directory structure for a larger organization (in other words, more than just a single address book as I am doing here), think hard about how you want the directory structured. You may want to add country codes (us, de, it, and so on) under your base distinguished name for a multinational company.

## Setting Up the OpenLDAP Server

All the software packages you need to set up an OpenLDAP server are included with Fedora. As an alternative, you can easily install the packages over the Internet using yum. With those packages installed, you can start configuring your OpenLDAP server.

### Installing OpenLDAP packages

To configure your OpenLDAP server, start by installing all the openldap packages from Fedora. First, check which openldap packages are installed:

```bash
# rpm -qa "openldap*"
```

You need the openldap-devel package only if you are developing LDAP applications. Otherwise, you can install the openldap, openldap-clients, and openldap-servers packages from the DVD that comes with this book or over the Internet by typing:

```bash
# yum install openldap openldap-clients openldap-servers
```

### Configuring the OpenLDAP server (slapd.conf)

You configure the access and use of your OpenLDAP databases in the configuration file, `/etc/openldap/slapd.conf`. As an alternative, you could instead add your slapd.conf to a database of information in the `/etc/openldap/slapd.d` directory. This procedure uses the older `slapd.conf` method.

> NOTE: For a more complete description on features you can use in your `slapd.conf` file, refer to the slapd.conf man page.

1. **Remove the slapd.d directory.** If you like, you can convert your `slapd.conf` file to be stored in the `/etc/openldap/slapd.d` directory (refer to the slaptest man page for information on converting that file to the newer file formats). To use the older style `slapd.conf` file, remove the `slapd.d` directory as follows:

   ```bash
   # rm -rf /etc/openldap/slapd.d
   ```

2. **Edit slapd.conf.** Make a backup copy of the `/etc/openldap/slapd.conf` file and then open the file as root user, using any text editor. The following steps tell you some of the information you might want to change.

3. **Review the schemas.** In the `slapd.conf` file, schemas that are generally useful for creating LDAP directories are included from the `/etc/openldap/schema` directory. Other schemas you might use will often rely on these schemas’ being included. So, unless you know you don’t need them, don’t delete any of these schemas:

   ```text
   include /etc/openldap/schema/corba.schema
   include /etc/openldap/schema/core.schema
   include /etc/openldap/schema/cosine.schema
   include /etc/openldap/schema/duconf.schema
   include /etc/openldap/schema/dyngroup.schema
   include /etc/openldap/schema/inetorgperson.schema
   include /etc/openldap/schema/java.schema
   include /etc/openldap/schema/misc.schema
   include /etc/openldap/schema/nis.schema
   include /etc/openldap/schema/openssl.schema
   include /etc/openldap/schema/policy.schema
   include /etc/openldap/schema/collective.schema
   ```

Because schemas are plain text files, you can open them with any text editor. Several sections of the schema are of interest to us. The `corba.schema` file is required for all LDAP directories. The `cosine.schema` and `inetorgperson.schema` files are particularly useful (and needed for this procedure). The `nis.schema` file is used to provide Network Information Service (NIS) data in an LDAP directory.
