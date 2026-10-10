![](bbox=[0.25, 0.1, 0.81, 0.39])

Figure 22-2: Search an LDAP address book directory by name, e-mail address, or other information.

# Summary

Lightweight Directory Access Protocol (LDAP) is a popular tool for creating directories of information that need to be accessed by a variety of different network-ready applications. LDAP is based on the CCITT X.500 standard, but provides a more workable subset of those features for creating directories of information that needs to be highly accessible.

In Fedora and RHEL systems, OpenLDAP is included for you to use if you want to offer LDAP services from your computer. To configure an LDAP server, you need to set up the slappd.conf file (to configure the slappd daemon) and create entries that are then loaded into your LDAP directory files. Those entries are typically added to a file in LDIF format and loaded into files in the /var/lib/ldap directory by the ldapadd command.

To check the address book created by the example in this chapter, you can use the Thunderbird e-mail client. Using Thunderbird, or other LDAP-enabled e-mail application, you can search the LDAP directory for names, e-mail addresses and other information contained in that directory.