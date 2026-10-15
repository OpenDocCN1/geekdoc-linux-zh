
| File | Description |
|---|---|
| /var/spool/mail | Incoming mail. |
| /var/spool/mqueue | Outgoing mail. |
| /var/spool/maillog | Mail log file. |

TABLE 24-2 Sendmail Files and Directories (continued)

> NOTE If your mail server services several hosts, you will need to enter them in the /etc/mail/local-host-names file.

## Aliases and LDAP

With Sendmail 8.10, Sendmail can now support the Lightweight Directory Access Protocol (LDAP). LDAP enables the use of a separate server to manage Sendmail queries about user mail addresses. Instead of maintaining aliases and virtusertable files on different servers, Sendmail uses LDAP support to simply use one centralized LDAP server to locate recipients. Mail addresses are looked up in the LDAP server, instead of having to search several aliases and virtusertable files on different servers. LDAP also provides secure authentication of users, allowing controlled access to mail accounts. The following example enables LDAP support on Sendmail in the sendmail.mc file:

```
FEATURE(`ldap_routing')dnl
LDAPROUTE_DOMAIN(`mytrek.com')dnl
```

Alternatively, Sendmail still supports the use of aliases, for either sent or received mail. It checks an aliases database file called aliases.db that holds alias names and their associated e-mail addresses. This is often used for administrator mail, where mail may be sent to the system's root user and then redirected to the mail address of the actual system administrator. You can also alias host addresses, enabling you to address hosts on your network using only their aliases. Alias entries are kept in the /etc/aliases file. This file consists of one-line alias records associating aliases with user addresses. You can edit this file to add new entries or to change old ones. They are then stored for lookup in the aliases.db file using the command newaliases, which runs Sendmail with instructions to update the aliases.db file.

Aliases allow you to give different names for an e-mail address or collection of e-mail addresses. One of its most useful features is to create a mailing list of users. Mail addresses to an alias will be sent to the user or list of users associated with the alias. An alias entry consists of an alias name terminated by a colon and followed by a username or comma-separated list of users. For example, to alias filmcritic with the user george@rabbit.mytrek.com, you would use the following entry:

```
filmcritic:    george@rabbit.mytrek.com
```

To alias singers with the local users aleina and larisa, you would use

```
singers:    aleina, larisa
```

You can also use aliases as the target addresses, in which case they will expand to their respective user addresses. For example, the performers alias will expand through the filmcritic and singers aliases to the users george@rabbit.mytrek.com, aleina, and larisa.

```
performers:  filmcritic; singers
```

Once you have made your entries in the /etc/mail/aliases file, you need to generate a database version using the newaliases command:

```
newaliases
```

## Sendmail Configuration

The main Sendmail configuration file is sendmail.cf, located in the /etc directory. This file consists of a sometimes lengthy list of mail definitions that set general options, designate MTAs, and define the address rewrite rules. A series of options set features, such as maximum size of mail messages or the name of host files. The MTAs are those mailers through which Sendmail routes messages. The rewrite rules "rewrite" a mail address to route through the appropriate Internet connections to its destination (these rules can be complex). Check the Sendmail HOW-TO and the online documentation for a detailed explanation.

The sendmail.cf definitions can be complex and confusing. To simplify the configuration process, Sendmail supports the use of macros you can use to generate the sendmail.cf file using the m4 preprocessor (this requires installation of the sendmail-cf package). Macros are placed in the /etc/mail/sendmail.mc file. Here, you can use macros to designate the definitions and features you want for Sendmail, and then the macros are used to generate the appropriate definitions and rewrite rules in the sendmail.cf file. As part of the Sendmail package, several specialized versions of the sendmail.mc file are made available in the /usr/share/sendmail-cf directory. These begin with a system name and have the suffix .mc. On many distributions, a specialized version tailored to your distribution is already installed as your /etc/mail/sendmail.mc file.

Once you configure your sendmail.mc file, you use the following command to generate a sendmail.cf file (be sure first to back up your original sendmail.cf file). You can rename the sendmail.mc file to reflect the specific configuration. You can have as many different .mc files as you want and use them to implement different configurations.

```
m4 sendmail.mc > /etc/mail/sendmail.cf
```

You will then need to restart the Sendmail server to make the configuration effective:

```
service sendmail restart
```

In the sendmail.mc file, you configure different aspects of Sendmail using either a define command to set the value of Sendmail variables or a Sendmail macro that has already been defined to set a particular Sendmail feature. For example, to assign the PROCMail_PATH variable to the directory /usr/bin/procmail, you would use the following:
