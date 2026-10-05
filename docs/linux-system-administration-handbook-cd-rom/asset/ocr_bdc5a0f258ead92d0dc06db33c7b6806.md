# 98 Chapter 7 • E-mail

+   - Qmail also does not use /etc/aliases at all. There is a global way of setting up E-mail aliases, which is a bit easier to use. The alias user is used by q-mail to handle addresses that don't exist. For example, you could have \~alias/.qmail-markk contain the line

```
enry@wayage.net
```

to forward E-mail that comes in markk@wayage.net to
enry@wayage.net. A common use of this is setting up postmaster, abuse, or aliases.

+   - The root user does not receive E-mail. Due to the number of security problems this could cause, it was determined that root should be aliased to someone else (like the actual administrators of the machine). It makes cracking a root account much harder.

# Ezlm

The ezlm package allows for easy mailing list setups. It has all the functionality commonly needed in mailing list applications: automatic subscribe/unsubscribe, moderated lists, and digest creation (handled by ezlm-idx). Unlike many other mailing list applications, ezlm is command based—there should be no need for the mailing list administrator to edit files. Another feature of ezlm (and qmail) is that mailing list creation and administration do not require the root account.

By default, many of the ezlm programs get installed in /usr/local/bin/ezlm. The install instructions are in the INSTALL file (located in the ezlm-0.53 directory) and are also straightforward. Once installed and tested, users can create their own mailing lists with the following commands:

```
ezlm-make ~/list ~/.qmail-list user-list host
```

This creates the mailing list. The mailing list itself is contained in ~list. This mailing list is not moderated in that anyone can subscribe and unsubscribe. If you want a private mailing list where only the moderator can add or remove members, you can add the -P option. Once the mailing list is created, you can just remove ~list/public to create a moderated list or just create the file to create a public list:

```
ezlm-sub ~/list e-mail
```

This subscribes the E-mail to list. The new member is subscribed to the list.