# Installing the Mail Server

625

| Operator | Description |
| :--- | :--- |
| O | Assigns a value to an option. For example, `O AliasFile=/etc/aliases` defines the `AliasFile` option to `/etc/aliases`, which is the name of the `sendmail` alias file. |
| P | Defines values for the precedence field. For example, `Pjunky=-100` sets to -100 the precedence of messages marked with the header field `Precedence: junk`. |
| R | Defines a rule. (A rule has a left side and a right side; if input matches the left side, the right side replaces it. This rule is called *rewriting*.) For example, the rewriting rule `R$* ; $1` strips trailing semicolons. |
| S | Labels a rule set you can start defining with subsequent R control lines. For example, `Scanonify=3` labels the next ruleset as `canonify` or `ruleset 3`. |
| T | Adds a username to the trusted class (class t). For example, `Troot` adds `root` to the class of trusted users. |
| V | Defines the major version number of the configuration file. For example, `V1.0/Berkley` defines the version number as 1.0. |

# Other sendmail files

The `/etc/mail` directory contains other files that `sendmail` uses. These files are referenced in the `sendmail` configuration file, `/etc/mail/sendmail.cf` in `Fedora Core` and `/etc/sendmail.cf` in `SUSE`. For example, here's how you can search for the `/etc/mail` string in the `/etc/mail/sendmail.cf` file in `Fedora Core`:

```
grep "*​/etc/mail*​" /etc/mail/sendmail.cf
```

Here's what the `grep` command displays as a result of the search on my `Fedora Core` system:

```
Fw /etc/mail/local-host-names
PR-o /etc/mail/relay-domains
Kmailer table hash -o /etc/mail/mailertable.db
Kvirtuser hash -o /etc/mail/virtuser table.db
Kaccess hash -Tc<"MDF"> -o /etc/mail/access.db
#0 ErrorHeader=/etc/mail/error-header
0 HelpFile=/etc/mail/helpfile
O UserDatabaseSpec=/etc/mail/userdb.db
#0 ServiceSwitchFile=/etc/mail/service.switch
#0 DefaultAuthInfo=/etc/mail/default-auth-info
Pt /etc/mail/trusted-users
```

**Book VII**
**Chapter 4**

Managing Mail and News Servers