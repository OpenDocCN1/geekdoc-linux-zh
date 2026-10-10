your directory. Assuming that you kept your LDAP directory files in `/var/lib/ldap` and that it's okay to erase the whole database while you debug your entries, you can do the following:

> CAUTION: You're about to erase the LDAP directory files you created. Don't do this step if you have information in your LDAP directory files that is not in your ldif file. Don't erase your ldif file because you need it to recreate your directory files.

```
```bash
# /etc/init.d/ldap stop
# rm /var/lib/ldap/*
# /etc/init.d/ldap restart
# ldapadd -x -D "cn=Manager,dc=linxutoys,dc=net" -W -f toypeople.ldif
```
```

Repeat this process until you feel that your ldif file, and all the information it contains, has been properly loaded into your LDAP directory files.

At this point, you can decide if you need to further tune your LDAP directory (as described in the section “More ways to configure LDAP”). After that, I recommend that you check that your LDAP address book directory is working properly by trying to access it from Thunderbird, using its Contacts feature (as described later in this chapter).

# ## More Ways to Configure LDAP

If you plan to scale up your LDAP directory to be used by more than just a small office or home e-mail server, there are some additional configuration options you might want to consider. Here are a few suggestions:

+   • Replicate the LDAP directory — You can make your LDAP directory accessible from multiple LDAP servers and have updates to your directory be disseminated to those servers. See the man page for the slurpd daemon (which handles update replication) and the OpenLDAP Administrator’s Guide for information on setting up LDAP directory replication (`/usr/share/doc/openldap-servers/guide.html`).

+   • Add certificates — Transport Layer Security is built into the OpenLDAP server. For information on defining certificates and ciphers that will be accepted by the slapd daemon, refer to the slapd.conf man page.

+   • Change log levels — You can specify the level of debugging that is done by the slapd daemon. By adding the loglevel `<integer>` option to the slapd.conf file, you can have slapd do the following types of logging:

+   1   Trace function calls
+   2   Debug packet handling
+   4   Heavy trace debugging
+   8   Connection management