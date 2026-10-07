restrictions.

**Note** To have sendmail function as a relay, it must also be configured to receive mail. You may need to tweak your configuration to allow this, as described in the section "Receiving Mail."

To allow sendmail to relay mail from certain classes of computers, you must add a FEATURE line to sendmail.mc or its equivalent file. This FEATURE line includes one of the following options:

+   promiscuous_relay *This extremely dangerous option tells sendmail to relay any mail that comes its way. Don't use this option, because it virtually guarantees that spammers will, sooner or later, abuse your system.*

+   relay_based_on_MX *This option configures sendmail to accept relays from other computers, so long as those computers' domains are configured to show your system as the MX. This option is fairly lax on security, because it essentially lets somebody else (whoever controls the DNS server for the remote system) determine whether your system will function as a relay.*

+   relay_entire_domain *If you set this option, sendmail accepts mail from any host within the domain to which it belongs. This can be a convenient way to quickly configure a Linux system as a limited mail relay.*

+   relay_local_from *This option tells sendmail to accept relays if the sender uses the server's address as its own. This can be convenient in some cases, but it's also easily abused.*

+   relay_hosts_only *This option works with an access database (described shortly) to allow you to list individual hosts as acceptable or unacceptable for relaying.*

+   access_db *This feature allows you to use an access database (described shortly) to list domains for which sendmail will relay.*

As an example, the default sendmail.mc file for Red Hat includes the following line:

```
FEATURE(`access_db',`hash -o /etc/mail/access.db')dnl
```

You can modify this line to use some other relay option, if one is appropriate for your network. Alternatively, you can adjust the access database file. This file is called /etc/mail/access on Red Hat 7.3, but it may appear elsewhere on some distributions. The file consists of lines, each containing a single domain name, machine name, or IP address followed by a tag that indicates how sendmail will treat messages received from the sender. (Lines beginning with pound signs [#] are comments and are ignored.) The default Red Hat 7.3 configuration looks like this:

```
# by default we allow relaying from localhost...
localhost.localdomain	RELAY
localhost	RELAY
127.0.0.1	RELAY
```

Valid tags are as follows:

+   **OK** Forces sendmail to accept the mail, even if other rules would reject it.

+   **RELAY** Accepts for relay mail that comes from or goes to the specified domain. The

356