
## Chapter 11. Email

/etc/mail/sendmail.mc, back up the original /etc/mail/sendmail.cf, and then use the included m4 macro processor to create a new /etc/mail/sendmail.cf. More information on configuring Sendmail can be found in Section 11.3.1.3 Common Sendmail Configuration Changes. Various Sendmail configuration files are installed in the /etc/mail/ directory including:

- access — Specifies systems that use Sendmail for outbound mail.
- domatable — Specifies domain name mapping.
- local-host-names — Specifies aliases for the host.
- mailertable — Specifies instructions that override routing for particular domains.
- virtualtable — Specifies a domain-specific format of aliasing, allowing multiple virtual domains to be hosted on one machine.

Several of the configuration files in /etc/mail/, as access, domatable, mailertable and virtualtable, actually store their information in database files before Sendmail can use any changes. To include any changes made to these database files, run the command:

```bash
makemap hash /etc/mail/<name> < /etc/mail/<name>
```

Where <name> is replaced with the name of the configuration file to convert.
For example, to have all addresses addressed to the example.com domain delivered to <bob@other-example.com>, add the following line to the virtualtable file:

```
@example.com bob@other-example.com
```

To finalize the change, the virtualtable.db file must be updated using the following command as root:

```bash
makemap hash /etc/mail/virtualtable < /etc/mail/virtualtable
```

This creates a new virtualtable.db file containing the new configuration.

### 11.3.1.3. Common Sendmail Configuration Changes

When altering the Sendmail configuration file, it is best to generate an entirely new /etc/mail/sendmail.cf instead of editing an existing one.

![](img/31025704b51d5760c0228ff0f3db98bf_166_0.png)

**Caution**

Before changing the sendmail.cf file, it is a good idea to backup a working version of the file.

To add the desired functionality to Sendmail, edit the /etc/mail/sendmail.mc file. When finished, use the m4 macro processor to generate a new sendmail.cf by executing the m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf command. After creating a new /etc/mail/sendmail.cf file, restart Sendmail to make it take effect. The easiest way to do this is to type the /sbin/service sendmail restart as command root.

By default, the m4 macro processor is installed with Sendmail but is part of the m4 package.

## Chapter 11. Email

**Important**

The default sendmail.cf file does not allow Sendmail to accept network connections from any other host than the local computer. Configure Sendmail as a server for other clients, edit /etc/sendmail.cf and change DAEMON_OPTIONS to listen on network devices or comment out this option if needed. Then regenerate /etc/mail/sendmail.cf by running:

```bash
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

This configuration will work for most SMTP-only sites. It will not work for UUCP (UNIX to UNIX Copy); you must generate a new sendmail.cf if using UUCP mail transfers.

Consult the /usr/share/sendmail-cf/README file before editing any files in the directories under the /usr/share/sendmail-cf directory, as they can affect the future configuration of /etc/mail/sendmail.cf files.

### 11.3.1.4. Masquerading

One common Sendmail configuration is to have a single machine as a mail gateway for all machines on the network. For instance, a company may want to have a mail called mail.bigcorp.com that handles all of their email and assigns a return address to all going mail.

In this situation, the Sendmail server must masquerade the machine names on the company network so their return address is user@bigcorp.com instead of devel@bigcorp.com.

To do this, add the following lines to /etc/mail/sendmail.mc:

```
FEATURE(always_addr_domain) dnl
FEATURE('masquerade_entire_domain')
FEATURE('masquerade_envelope')
FEATURE('masquerade')
MASQUERADE_AS('bigcorp.com.')
MASQUERADE_DOMAIN('bigcorp.com.')
MASQUERADE_AS (bigcorp)
```

After generating a new sendmail.cf using m4, this configuration will make all mail from inside the network appear as if it were sent from bigcorp.com.

### 11.3.1.5 Stopping Spam

Email spam can be defined as unwanted and unwanted email received by a user who never requested the communication. It is a disruptive, costly, and widespread abuse of Internet communication standards.

Sendmail makes it relatively difficult to block new spamming techniques by sending junk email. It blocks many of the user spamming methods by default.

For example, forwarding of SMTP messages, also called relay, has been disabled by default since Sendmail 8.9. Before this change, Sendmail would relay the mail host (x.org) to accept messages from any user (y.com) and send them to a different user (z.net). Now, however, Sendmail must be configured to permit any domain to relay through the server. To relay domains, edit the /etc/mail/relay-domains file and restart Sendmail.

However, many times users are bombarded with spam from other servers throughout the Internet. In these instances, Sendmail's access control features available through the /etc/mail/access file can be used to prevent connections from unwanted hosts. The following example illustrates how this file can be used both block and specifically allow access to the Sendmail server:

```
badspammer.com ERROR:550 "Go away and do not spam us anymore"
tux.badspammer.com OK
10.0 RELAY
```

This example states that any email sent from badspammer.com is blocked with a 550 RFC-821 compliant error code, with a message sent to the spammer. Email sent from the tux.badspammer.com sub-domain, which would be accepted. The last line sent from the 10.0.* is relayed through the mail server.

Because /etc/mail/accessdb is a database, use makemap to activate any changes. Do this with the following command as:

```bash
makemap hash /etc/mail/access < /etc/mail/access
```

This example only scratches the surface of what Sendmail can do in terms of allowing or blocking access. Use the /usr/share/doc/sendmail/README.cf for more information and examples.

Since Sendmail can handle much when delivering mail, it is also possible to use a spam filtering program, such as SpamAssassin to identify and filter spam for users. Refer to Section 11.4.2.6 Spam Filters for more details on applications.

### 11.3.1.6. Using Sendmail with LDAP

Using the Lightweight Directory Access Protocol (LDAP) is a quick and powerful way to find specific information about a particular user from a larger group. For example, an LDAP server can be used to look up a particular email address from a common corporate department by the user's name. In this kind of implementation, LDAP is largely separate from Sendmail, with LDAP storing the hierarchical information and Sendmail only delivering messages.

However Sendmail supports a much greater integration with LDAP, where LDAP to replace separated files, as aliases and virtualtables, on different mail servers that work to support a medium- to enterprise-level organization. In short, LDAP abstracts the main routing from Sendmail and its separate configuration files to a powerful LDAP cluster that can be leveraged by different applications.

The current version of Sendmail contains support for LDAP. To extend the Sendmail server using LDAP, first as OpenLDAP, running and properly configured. Then edit the /etc/mail/sendmail.mc to include the following:

```
LDAPROUTE_DOMAIN('yourdomain.com')dnl
FEATURE('ldap_routing')dnl
```

![](img/31025704b51d5760c0228ff0f3db98bf_168_0.png)

**Note**

This is for a very basic configuration of Sendmail with LDAP. Your configuration should differ greatly from this depending on the implementation of LDAP, especially when configuring several Sendmail machines to use a common LDAP server.

Consult /usr/share/doc/sendmail/README.cf for detailed LDAP routing configuration instructions and examples.

Next, recreate the /etc/mail/sendmail.cf file by running m4 and restarting Sendmail. See Section 11.3.1.3 Common Sendmail Configuration Changes for instructions on doing this.
