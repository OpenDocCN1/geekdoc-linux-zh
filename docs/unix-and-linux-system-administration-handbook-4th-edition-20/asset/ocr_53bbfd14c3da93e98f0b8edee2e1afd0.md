# Chapter 20

# Electronic Mail

In /etc/mail/admin.com/virtual we could then have the lines

postmaster@admin.com evi, david@admin.com
david@admin.com david@schweikert.ch
evi@admin.com evi

Mail for evi@admin.com would be redirected to evi@cs.colorado.edu (myorigin is appended) and would ultimately be delivered to the mailbox of evi because cs.colorado.edu is included in mydestination.

Definitions can be recursive: the right hand side can contain addresses that are further defined on the left hand side. Note that the right hand side can only be a list of addresses. If you need to use an external program or to include: files, then you need to redirect the email to an alias, which can then be expanded to your yards.

To keep everything in one file, you can set virtual_alias_domains to the same lookup table as virtual_alias_maps and put a special entry in the table to mark it as a virtual alias domain. In main.cf:

```
virtual_alias_domains = $virtual_alias_maps
virtual_alias_maps = hash/etc/mail/admin.com/virtual
```

In /etc/mail/admin.com/virtual:

```
admin.com notused
postmaster@admin.com evi, david@admin.com
```

The right side of the entry for the mail domain (admin.com) is never actually used; admin.com's existence in the table as an independent entry is enough to make Postfix consider it a virtual alias domain.

# Virtual mailbox domains

Domains listed under virtual_mailbox_domains are similar to local domains, but the list of users and their corresponding mailboxes must be managed independently of the system's user accounts.

The parameter virtual_mailbox_maps points to a table that lists all valid users in the domain. The map format is

```
user@domain /path/to/mailbox
```

If the path starts with a slash, the mailboxes are stored in Mailird format. The value of virtual_mailbox_base is always prefixed to the specified paths.

You want to alias some of the addresses in the virtual mailbox domain. Use a virtual_alias_map to do this here. Here is a complete example. In main.cf:

```
virtual_mailbox_domains = admin.com
virtual_mailbox_base = /var/mail/virtual
virtual_mailbox_maps = hash/etc/mail/admin.com/vmailboxes
virtual_alias_maps = hash/etc/mail/admin.com/varialiases
```

836