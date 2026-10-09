Each line except the first specifies an attribute. The word on each line preceding the colon is the attribute name. Following the colon and a SPACE is the attribute value. The first line in this example specifies the DN of the entry. The attribute value used in the RDN is a CN (Common Name) from the entry: **Sam the Great**. This second-level entry is a child of the top-level entry; thus the DN of the parent entry is the DN of the top-level entry (**dc=brillserve,dc=com**). You can uniquely identify this entry by its DN: **cn=Sam the Great,dc=brillserve,dc=com**. Because this entry defines two CNs, a search for *Sam the Great* or *The Great* will return this entry. This entry also defines a given name, a surname (sn), an email address (mail), and other attributes.

+   objectClass attribute Entries inherit object class attributes from their parents. In addition, each entry must have at least one **objectClass** attribute. Each **objectClass** value must be a class defined in the schema. The schema specifies both mandatory and optional [allowed] attributes for an object class. For example, the following entry in the schema defines the object class named *person*. The **MUST** and **MAY** lines specify which attributes the *person* object class requires (sn [surname] and cn; attribute names are separated by a dollar sign) and which attributes are optional (userPassword, *telephoneNumber*, *seeAlso*, and *description*).

```
$ cat /etc/openldap/schema/core.schema  
...
objectClass ( 2 . 5 . 6 . 6  NAME 'person'  
	DESC 'RFC2256: a person'  
	SUP top STRUCTURAL  
	MUST ( sn $ cn )  
	MAY ( userPassword $ telephoneNumber $ seeAlso $ description ) )  
...
```

+   Abbreviations The following list summarizes the abbreviations covered in this section.  
+   **CN** Common Name  
+   **DC** Domain Component  
+   **DN** Distinguished Name  
+   **DSE** DSA-Specific Entry  
+   **LDIF** LDAP Data Interchange Format  
+   **RDN** Relative Distinguished Name

# MORE INFORMATION

+   Local man pages: ldap.conf, *ldapmodify*, *ldapsearch*, ldif, slapd, slapd.conf, *slappassword*

+   Web LDAP home page: www.openldap.org

+   Administrator's Guide: www.openldap.org/doc/admin24

+   389 Directory Server home page: directory.fedoraproject.org

+   Red Hat Directory Server manuals: access.redhat.com/site/documentation/

+   Red_Hat_Directory_Server (these manuals apply to both the Fedora and Red Hat Directory Servers)

+   OpenLDAP Faq-O-Matic: www.openldap.org/faq

+   book: www.zytrax.com/books/ldap

+   gq: sourceforge.net/projects/gqclient

+   HOWTO LDAP *Linux HOWTO*