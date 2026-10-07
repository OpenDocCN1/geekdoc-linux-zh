Sendmail aliases perform important functions that are an essential part of creating a mail server. Mail aliases do the following:

+   Specify nicknames for individual users. Nicknames can be used to direct mail addressed to special names, such as postmaster or root, to the real users that do jobs. Aliases can simplify creation of a standard e-mail address structure for a domain because mail aliases have a more flexible structure than logins.

+   Forward mail to other hosts. Sendmail aliases automatically forward mail to the host address included as part of the recipient address.

+   Define mailing lists. An alias with multiple recipients is a mailing list.

Mail aliases are defined in the aliases file. The location of the aliases file is set by the ALIAS_FILE define in the Sendmail configuration. The redhat.mc configuration file in Chapter 5 uses ALIAS_FILE to set the location of the aliases file /etc/aliases. By default, Sendmail 8.11 locates the file in the /etc/mail directory (/etc/mail/aliases). Regardless of where it is located, the basic format of entries in the aliases file is:

```
alias: recipient
```

The alias is the username from the e-mail address, and recipient is the name to which the mail should be delivered. The recipient field can contain a username, another alias, or a full e-mail address containing both a username and a hostname. Additionally, there can be multiple recipients for a single alias to create a mailing list. The aliases file delivered with a Red Hat system, with few additions to illustrate the full range of uses for aliases, is shown in Listing 6.5.

# Listing 6.5 The Basic Red Hat aliases Database

```
#
# @(#aliases 8.2 (Berkeley) 3/5/94
# Aliases in this file will NOT be expanded in the header from
# Mail, but WILL be visible over networks or from /bin/mail.
#n# >>>>>>> The program "newaliases" must be run after
# >> NOTE >> this file is updated for any changes to
# >>>>>>> show through to sendmail.
```

```
# Basic system aliases -- these MUST be present.
MAILER-DAEMON: postmaster
postmaster: root
```