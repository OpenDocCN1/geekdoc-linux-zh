
| Operator | Description |
| :--- | :--- |
| O | Assigns a value to an option. For example, O AliasFile=/etc/aliases defines the AliasFile option to /etc/aliases, which is the name of the sendmail alias file. |
| P | Defines values for the precedence field. For example, P junk=-100 sets to -100 the precedence of messages marked with the header field Precedence: junk. |
| R | Defines a rule. (A rule has a left side and a right side; if input matches the left side, the right side replaces it. This rule is called rewriting.) For example, the rewriting rule R $* : $1 strips trailing semicolons. |
| S | Labels a ruleset you can start defining with subsequent R control lines. For example, S canonify=3 labels the next ruleset as canonify or ruleset 3. |
| T | Adds a username to the trusted class (class t). For example, T root adds root to the class of trusted users. |
| V | Defines the major version number of the configuration file. For example, V 10/Berkeley defines the version number as 10. |

## Other sendmail files

The /etc/mail directory contains other files that sendmail uses. These files are referenced in the sendmail configuration file, /etc/mail/sendmail.cf in Fedora Core and /etc/sendmail.cf in SUSE. For example, here’s how you can search for the /etc/mail string in the /etc/mail/sendmail.cf file in Fedora Core:

```
grep "/etc/mail" /etc/mail/sendmail.cf
```

Here’s what the grep command displays as a result of the search on my Fedora Core system:

```
Pw/etc/mail/local-host-names
PR-o /etc/mail/relay-domains
Kmailer table hash -o /etc/mail/mailertable.db
Kvirth user hash -o /etc/mail/virthuser table.db
Kaccess hash -To<TMPF> -o /etc/mail/access.db
#0 ErrorHeader=/etc/mail/error-header
O HelpFile=/etc/mail/helpfile
O UserDatabaseSpec=/etc/mail/userdb.db
#0 ServiceSwitchFile=/etc/mail/service.switch
#0 DefaultAuthInfo=/etc/mail/default-auth-info
Pt/etc/mail/trusted-users
```

You can ignore the lines that begin with a hash mark or number sign (#) because sendmail treats those lines as comments. The other lines are sendmail control lines that refer to other files in the /etc/mail directory.

Here's what some of these sendmail files are supposed to contain. (Note that not all of these files have to be present in the /etc/mail directory, and even when present, some files may be empty.)

- /etc/mail/access: Names and/or IP addresses of hosts allowed to send mail (useful in stopping spam — unwanted e-mail)
- /etc/mail/access.db: Access database generated from the /etc/mail/access file
- /etc/mail/helpfile: Help information for SMTP commands
- /etc/mail/local-host-names: Names by which this host is known
- /etc/mail/mailertable: Mailer table used to override how mail is routed (For example, the entry comcast.net comcast:smtp.comcast.net tells sendmail that mail addressed to comcast.net has to be sent to smtp.comcast.net.)
- /etc/mail/relay-domains: Hosts that permit relaying
- /etc/mail/trusted-users: List of users allowed to send mail using other user's names without a warning
- /etc/mail/userdb.db: User database file containing information about each user's login name and real name
- /etc/mail/virtusertable: Database of users with virtual-domain addresses hosted on this system

![](img/11709a8f88c8cd03868a929dc94c0e2b_651_0.png)

The /etc/mail directory sometimes contains other files —/etc/mail/certs and the files with the .pem extension — that are meant for supporting Privacy Enhanced Mail (PEM) in sendmail by using the STARTTLS extension to SMTP. The STARTTLS extension uses TLS (more commonly known as SSL — Secure Sockets Layer) to authenticate the sender and encrypt mail. RFC 2487 describes STARTTLS. (This RFC is available online at http://ietf.org/rfc/rfc2487.txt.)

If you edit the /etc/mail/mailertable file, you have to type the following command before the changes take effect:

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_651_1.png)

Here is an easier way to make sure that you rebuild everything necessary after making any changes — just type the following commands while logged in as root:

```
cd /etc/mail
make
```

The first command changes the current directory to /etc/mail and the second command runs the make command, which reads a file named Makefile in /etc/mail to perform the steps necessary to rebuild everything. (To learn more about make and Makefile, see Book VIII, Chapter 1.)

## The .forward file

Users can redirect their own mail by placing a .forward file in their home directory. The .forward file is a plain-text file with a comma-separated list of mail addresses. Any mail sent to the user is instead forwarded to these addresses. If the .forward file contains a single address, all e-mail for that user is redirected to that single e-mail address. For example, suppose a .forward file containing the following line is placed in the home directory of a user named emily:

ashley

This line causes sendmail to automatically send all e-mail addressed to emily to the username ashley on the same system. User emily does not receive mail at all.

You can also forward mail to a username on another system by listing a complete e-mail address. For example, I added a .forward file with the following line to send my messages (addressed to my username, naba) to the mail address naba@comcast.net:

naba@comcast.net

Now suppose I want to keep a copy of the message on the original system, in addition to forwarding to the address naba@comcast.net. I can do so by adding the following line to the .forward file:

naba@comcast.net, naba\

I simply append my username and end the line with a backslash. The backslash (\) at the end of the line stops sendmail from repeatedly forwarding the message (because when a copy is sent to my username on the system, sendmail would normally process my .forward file again). The backslash tells sendmail not to forward the message repeatedly.

![](img/11709a8f88c8cd03868a929dc94c0e2b_652_0.png)

In addition to the sendmail.cf file, sendmail also consults an alias file named /etc/aliases to convert a name into an address. The location of the alias file appears in the sendmail configuration file.

Each alias is typically a shorter name for an e-mail address. The system administrator uses the sendmail alias file to forward mail, to create a mailing list (a single alias that identifies several users), or to refer to a user by several different names. For example, here are some typical aliases:

barkakati: naba
naba: naba@lnbsoft
all: naba, leha, ivy, emily, ashley

The first line says that mail addressed to barkakati is delivered to the user named naba on the local system. The second line indicates that mail for naba really is sent to the username naba on the lnbsoft system. The last line defines all as the alias for the five users naba, leha, ivy, emily, and ashley. That means mail sent to all goes to these five users.

After defining any new aliases in the /etc/aliases file, you must log in as root and make the new alias active by typing the following command:

sendmail -bi

## Installing the INN Server

In this section, I describe how to configure the InterNetNews (INN), a TCP/IP-based news server. First you have to install INN.

In Debian, MEPIS, Ubuntu, and Xandros, type dpkg -l inn* to see if inn is installed. In Fedora Core and SUSE, type rpm -q inn and see if the inn package is installed.

In Debian, MEPIS, and Ubuntu, type apt-get install inn to install the INN server. In Fedora Core, log in as root, mount the DVD, and type cd /media/cdrom/Fedora/RPMS followed by rpm -vh inn*. In SUSE, click Software Management in the YaST Control Center’s Software category. Then use YaST’s search feature to look for inn, select the relevant packages from the search results, and install them. In Xandros, first run Xandros Networks, choose Edit>Set Application Sources, and click the Debian Unsupported Site link as a source. Then type apt-get install inn to install the INN server.

![](img/11709a8f88c8cd03868a929dc94c0e2b_653_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_653_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_653_2.png)
