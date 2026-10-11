The following steps describe how to make Samba PDC users members of the Domain Admins group.

+   1. Create a UNIX group (usually in /etc/group); let’s call it domadm.

+   2. Add to this group the users that must be “Administrators”. For example, if you want joe, john, and mary to be administrators, your entry in /etc/group will look like this:

```
domadm:x:502:joe,john,mary
```

+   3. Map this domadm group to the “Domain Admins” group by running the command:

```
root# net groupmap add ngroup=“Domain Admins” unixgroup=domadm
```

The quotes around “Domain Admins” are necessary due to the space in the group name. Also make sure to leave no white space surrounding the equal character (=). Now joe, john, and mary are domain administrators.

It is possible to map any arbitrary UNIX group to any Windows NT4/200x group as well as to make any UNIX group a Windows domain group. For example, if you wanted to include a UNIX group (e.g., acct) in an ACL on a local file or printer on a Domain Member machine, you would flag that group as a domain group by running the following on the Samba PDC:

```
root# net groupmap add rid=1000 ngroup=“Accounting” unixgroup=acct
```

The ngroup value must be in quotes if it contains space characters to prevent the space from being interpreted as a command delimiter.

Be aware that the RID parameter is an unsigned 32-bit integer that should normally start at 1000. However, this RID must not overlap with any RID assigned to a user. Verification for this is done differently depending on the passdb backend you are using. Future versions of the tools may perform the verification automatically, but for now the burden is on you.

# 11.2.1 Warning: User Private Group Problems

Windows does not permit user and group accounts to have the same name. This has serious implications for all sites that use private group accounts. A private group account is an administrative practice whereby users are each given their own group account. Red Hat Linux, as well as several free distributions of Linux, by default create private groups.

When mapping a UNIX/Linux group to a Windows group account, all conflict can be avoided by assuring that the Windows domain group name does not overlap with any user account name.