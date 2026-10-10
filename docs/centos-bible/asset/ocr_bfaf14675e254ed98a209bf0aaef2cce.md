# Structuring Your LDAP Directories

While standards documents are used to keep the object classes, attributes, and other elements of LDAP directories unique, you are free to put together those elements into your own LDAP directories however you want. The structure you use to create your LDAP databases is the LDAP Data Interchange Format (LDIF).

Every piece of information you store in your LDAP directory must fall under a base distinguished name (or base dn). Because many organizations these days can be represented by a unique Internet domain name, the domain name is a popular way to identify your LDAP base dn. In fact, for the examples in this chapter, the base distinguished name I use is example.com. If you are creating an LDAP directory for an organization that can be represented by a domain name, you can replace example.com with your domain name.

If you are creating an LDAP directory structure for a larger organization (in other words, more than just a single address book as I am doing here), you need to think hard about how you want the directory structured. You may want to add country codes (us, de, it, etc.) under your base distinguished name for a multinational company.

# Setting Up the OpenLDAP Server

All the software packages you need to set up an OpenLDAP server are included on the DVD that comes with CentOS distributions. As an alternative, you can easily install the packages over the Internet using yum. With those packages installed, you can start configuring your OpenLDAP server.

# Installing OpenLDAP Packages

To configure your OpenLDAP server, you should start by installing all the openldap packages from your CentOS distribution. First, check which OpenLDAP packages are installed:

```
# rpm -qa "openldap*"
```

You need the openldap-devel package only if you are developing LDAP applications. Otherwise, you can install the openldap, openldap-clients, and openldap-servers packages from the DVD that comes with this book.

# Configuring the OpenLDAP Server (slapd.conf)

You configure the access and use of your OpenLDAP databases in the configuration file, /etc/openldap/slapd.conf.

> For a more complete description of features that you can use in your slapd.conf file, refer to the slapd.conf man page.