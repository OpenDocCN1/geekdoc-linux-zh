
## Other — control lines are even easier to understand

For example, the line:

```
- O Helpfile=/etc/mail/helpfile
```

defines the option `HelpFile` as the filename `/etc/mail/helpfile`. That file contains help information sendmail uses when it receives a `HELP` command.

Table 4-1 summarizes the one-letter operators used in `sendmail.cf`. Each entry also shows an example of that operator. This table should help you understand some of the lines in `sendmail.cf`.

| Table 4-1 Control Operators Used in sendmail.cf |
| Operator | Description |
| C | Defines a class, a variable (think of it as a set) that can contain several values. For example, `Clocalhost` adds the name `localhost` to the class `w`. |
| D | Defines a macro, a name associated with a single value. For example, `DNMailer=DAEMON` defines the macro `n` as `MAILER-DAEMON`. |
| F | Defines a class that's read from a file. For example, `Fw=/etc/mail/local-host-names` names the hosts from the file `/etc/mail/local-host-names` and adds them to the class `w`. |
| H | Defines the format of header lines that sendmail inserts into a message. For example, `HP2Return-Path: \<sg>` defines the `Return-Path:` field of the header. |
| K | Defines a macro key-value database. For example, `Karith` defines the mapped name as the compiled-in mail of the same name. |
| M | Specifies a mailer. The following lines define the procmail mailer: `Mprocmail.P=/usr/bin/procmail,R=DFMSphnu9,S=EnvSMTP/HdrFromSMTP,R=EnvSMTP/HdrFromSMTP,T=DNS/RFC822/X-Unix,A=procmail -Y -m $f $h $u` |
| 0 | Assigns a value to an option. For example, `0 AliasFile=/etc/aliases` defines the `AliasFile` to `/etc/aliases`, which is the name of the sendmail alias file. |
| P | Defines values for the precedence field. For example, `Pjunk=-100` sets to `-100` the precedence of messages with the header field `Precedence: junk`. |
| R | Defines a rule (a rule has a left-hand side and a right-hand side; if input matches the left-hand side, it's replaced by the right-hand side—this is called rewriting). For example, the rewriting rule `R* : $1` strips trailing semicolons. |
| S | Labels a rule as defining with control lines. For example, `Scanonify=3` labels the next rules as canonify or rules3. |
| T | Adds a name to the trusted class (class `t`). For example, `Toot` adds to the root of the trusted users. |
| V | Defines the major version of the configuration file. For example, `V10/Berkeley` defines the version number as `10`. |

### sendmail files

The `/etc/mail` directory contains other files that sendmail uses. These files are referenced in the sendmail configuration file, `/etc/mail/sendmail.cf`. For example, here's how you can search for the `/etc/mail` string in the `/etc/mail/sendmail.cf`:

```
grep "/etc/mail*" /etc/mail/sendmail.cf
```

Here's what the command displays as a result of the search on my Red Linux system:

```
w/etc/mail/local-hosts
FR -o /etc/mail/relay-domains
Kmailerhash -o /etc/mail/mailertable.db
Kvertuser -o /etc/mail/virtertable.db
Kcache hash -o <TMPF> -o /etc/mail/access.db
#0 Error-header=/etc/mail/error-header
#0 Helpfile=/etc/mail/helpfile
#0 Status=/etc/mail/statistics
#0 UserDatabaseSpec=/etc/mail/userdb.db
#0 ServiceSwitchFile=/etc/mail/service.switch
#0 DefaultAuthInfo=/etc/mail/default-auth-info
Ft/etc/mail/trusted-users
```

You ignore the lines that begin with a hash or number sign (`#`) because sendmail treats those as comments. The other lines are sendmail control lines that refer to other files in the `/etc/mail` directory.

Here's some of these sendmail files are supposed to contain (note that not all of these files have to be present in your `/etc/mail` directory, and even when present, some files may be empty):

- `/etc/mail/access` — Names or IP addresses of hosts allowed to send mail (in stopping spam unwanted)
- `/etc/mail/access.db` — Access database generated from `/etc/mail/access` file
- `/etc/mail/helpfile` — Help information for SMTP commands
- `/etc/mail/local-host-names` — Names by which host is known
