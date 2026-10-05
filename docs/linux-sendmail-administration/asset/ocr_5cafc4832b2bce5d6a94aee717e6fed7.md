# Appendix A m4 Macro Command Reference

matches the name of the feature. For example, mailertable defaults to the definition hash -o /etc/mail/mailertable. The database features are:

+   mailertable database maps host and domain names to specific mailer:table pairs. The mailer, host, triple is returned by ruleset 0 based on the delivery address. The mailertable allows you to define the mailer and the host of the delivery triple based on the domain name in the delivery address.

If the host or domain name in the delivery addresses matches a key field in the mailertable database, it returns the mailer and host for that address. The format of a mailertable entry is:

```
domain-name mailer:host
```

where domain-name is either a full hostname (plus domain) or a domain name. If a domain name is used, it will start with a dot (.), and it will match every host in the specified domain.

domaintable This database converts an old domain name to a new domain name. The old name is the key and the new value is the returned for the key.

bitdomain This database converts a BITNET hostname to an Internet hostname. The BITNET name is the key and the Internet hostname is the value returned. The bitdomain program that comes with the Sendmail distribution can be used to build this database. BITNET is obsolete.

uucdomain This converts a UUCP name to an Internet hostname. The key is the UUCP hostname and the value returned is the Internet hostname. This is useful if you still have users who e-mail using old UUCP addresses.

genericstable This database converts a e-mail address. The key to the database is either a username or a full e-mail address (username and hostname). The value returned by the database is the new e-mail address. genericstable is often used to convert the same addresses as those processed for masquerading, so the features affect masquerading and the genericable are set in the same way. See Chapter 9, "Special m4 Configurations", for an example of using the genericstable, and masquerading on the same addresses. If you use the genericstable and you use masquerading, set GENERIC_DOMAIN and GENERIC_DOMAIN_FILE to set the values you set for MASQUERADE_DOMAIN and MASQUERADE_DOMAIN_FILE.

virtertable This database aliases e-mail addresses. Essentially, this is an extended aliases database for aliasing addresses that are not local to this host. The key to the database is a full e-mail address or a domain name. The value returned by the database is the recipient address to which the mail is delivered. If a domain name is used as a key, it must begin with an at-sign (@). Mail addressed to