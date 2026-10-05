# OSTYPE macro

At first glance this command looks like a mistake that would cause the input file to be overwritten by an empty output file. However, makemap takes an appropriate suffix, so the actual output file is /etc/mail/access.db and in fact there is no conflict. Each time the text file is changed, the database file must be rebuilt with makemap (but sendmail need not be HUPed)

Comments appear in the text files from which maps are produced. They begin with # and continue until the end of the line.

In most circumstances, the longest possible match is used for database keys. With any hashed data structure, the order of entries in the input file is not significant. FEATUREs expect a database file as a default to hash as the database type and /etc/mail/tablename.db as the filename for the database.

# Generic macros and features

Table 20.10 lists common configuration primitives, whether they are typically used (yes, no, maybe), and a brief description of what they do. More details and examples are in the sections following the table.

# 20.10 Sendmail generic configuration primitives

| Primitive | Used? | Description |
| --- | --- | --- |
| OSTYPE | Yes | Includes OS-specific paths and mail flags |
| DOMAIN | No | Includes site-specific configuration details |
| MAILER | Yes | Enables mailers, typically smtp and local |
| FEATURE | Maybe | Enables a variety of sendmail features |
| use_cf | Yes (servers) | Lists hosts for which you accept mail |
| redirect | Maybe (servers) | Bounces mail nicely when users move |
| always_add_domain | Yes | Fully qualifies hostnames if UA is defined |
| access_db | Maybe (servers) | Sets database for hosts to relay mail |
| virtertable | Maybe (servers) | Turns on aliasing (virtual domains) |
| ldap_routing | Maybe (servers) | Routes incoming mail using LDAP |
| MASQUERADE_AS | Yes | Makes all mail seem to come from one place |
| EXPOSED_USER | Yes | Lists users who shouldn't be masqueraded |
| MAIL_HUB | Yes (servers) | Specifies mail server for incoming mail |
| SMART_HOST | Yes (clients) | Specifies mail server for outgoing mail |

# OSTYPE macro

An OSTYPE file packages a variety of vendor-specific information, such as the expected locations of mail-related files, paths to commands that sendmail needs, flags to see README for all of the variables that can be defined in an OSTYPE file.10

+   10. So where the OSTYPE is a file in the cf/m4 directory, which is magically prepended to your config file when you run the Build.

![](bbox=[0.95, 0.23, 0.99, 0.31])