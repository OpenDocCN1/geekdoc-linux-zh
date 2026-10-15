
In /etc/mail/admin.com/virtual we could then have the lines

```
postmaster@admin.com  evi, david@admin.com
david@admin.com        david@schweikert.ch
evi@admin.com          evi
```

Mail for evi@admin.com would be redirected to evi@cs.colorado.edu (myorigin is appended) and would ultimately be delivered to the mailbox of user evi because cs.colorado.edu is included in mydestination.

Definitions can be recursive: the right hand side can contain addresses that are further defined on the left hand side. Note that the right hand side can only be a list of addresses. If you need to execute an external program or to use :include: files, then you need to redirect the email to an alias, which can then be expanded according to your needs.

To keep everything in one file, you can set virtual_alias_domains to the same lookup table as virtual_alias_maps and put a special entry in the table to mark it as a virtual alias domain. In main.cf:

```
virtual_alias_domains = $virtual_alias_maps
virtual_alias_maps = hash:/etc/mail/admin.com/virtual
```

In /etc/mail/admin.com/virtual:

```
admin.com            notused
postmaster@admin.com  evi, david@admin.com
...
```

The right hand side of the entry for the mail domain (admin.com) is never actually used; admin.com's existence in the table as an independent entry is enough to make Postfix consider it a virtual alias domain.

## Virtual mailbox domains

Domains listed under virtual_mailbox_domains are similar to local domains, but the list of users and their corresponding mailboxes must be managed independently of the system's user accounts.

The parameter virtual_mailbox_maps points to a table that lists all valid users in the domain. The map format is

```
user@domain    /path/to/mailbox
```

If the path ends with a slash, the mailboxes are stored in Maildir format. The value of virtual_mailbox_base is always prefixed to the specified paths.

You often want to alias some of the addresses in the virtual mailbox domain. Use a virtual_alias_map to do this. Here is a complete example. In main.cf:

```
virtual_mailbox_domains = admin.com
virtual_mailbox_base = /var/mail/virtual
virtual_mailbox_maps = hash:/etc/mail/admin.com/vmailboxes
virtual_alias_maps = hash:/etc/mail/admin.com/valiases
```

/etc/mail/admin.com/vmailboxes might contain entries like these:

```
evi@admin.com      nemeth/evi/
```

/etc/mail/admin.com/valiases might contain:

```
postmaster@admin.com  evi@admin.com
```

You can use virtual alias maps even on addresses that are not virtual alias domains. Virtual alias maps let you redirect any address from any domain, independently of the type of the domain (canonical, virtual alias, or virtual mailbox). Since mailbox paths can only be put on the right hand side of the virtual mailbox map, use of this mechanism is the only way to set up aliases in that domain.

## Access control

Mail servers should relay mail for third parties only on behalf of trusted clients. If a mail server forwards mail from unknown clients to other servers, it is a so-called open relay, which is bad. See Relay control on page 791 for more details.

Fortunately, Postfix doesn't act as an open relay by default. In fact, its defaults are quite restrictive; you are more likely to need to liberalize the permissions than to tighten them. Access control for SMTP transactions is configured in Postfix through "access restriction lists." The parameters shown in Table 20.23 control what should be checked during the different phases of an SMTP session.

### Table 20.23 Postfix parameters for SMTP access restriction

| Parameter | When applied |
|---|---|
| smtpd_client_restrictions | On connection request |
| smtpd_helo_restrictions | On HELO/EHLO command (start of the session) |
| smtpd_sender_restrictions | On MAIL FROM command (sender specification) |
| smtpd_recipient_restrictions | On RCPT TO command (recipient specification) |
| smtpd_data_restrictions | On DATA command (mail body) |
| smtpd_etrn_restrictions | On ETRN commandᵃ |

a. This is a special command used for resending messages in the queue.

The most important parameter is smtpd_recipient_restrictions since access control is most easily performed when the recipient address is known and can be identified as being local or not. All the other parameters in Table 20.23 are empty in the default configuration. The default value is

```
smtpd_recipient_restrictions = permit_mynetworks, reject_unauth_destination
```

Each of the specified restrictions is tested in turn until a definitive decision about what to do with the mail is reached. Table 20.24 on the next page shows the common restrictions.
