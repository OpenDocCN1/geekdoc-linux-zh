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

# Sendmail Configuration

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