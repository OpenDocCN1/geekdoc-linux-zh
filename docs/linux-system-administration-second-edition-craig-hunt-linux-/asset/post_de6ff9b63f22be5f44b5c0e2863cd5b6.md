
You should change *desired-address.com* to the address you want to use as the return address, of course. The first line causes the From: header to change. This header is the one that most MUAs use to determine the sender and the address to which replies are sent. The FEATURE(*masquerade_envelope*) line causes sendmail to make additional header substitutions, which can be useful if an MUA uses a nonstandard header to determine the sender’s address. These options do not change the Received: headers, which are the most diagnostic for tracing mail back to its true source.

**Note** Some MUAs can change the From: header. Changing your sendmail configuration may therefore be overkill. If you set a From: address using an MUA, that setting overrides anything set using sendmail’s masquerading features.

## Configuring Relays

As described earlier, in “Push and Pull Protocols,” it’s common for an e-mail message to be relayed several times between its source and its destination. There’s a good chance you must cope with this situation in one way or another. In some cases, you may want or need to use an *outgoing relay*, in which your computer passes its mail to another system, which delivers the mail to its destination. In other cases, you may need to configure a computer so that it *functions* as an outgoing relay; other computers (such as mail clients on your own domain) connect to your Linux box to send their mail. Each configuration requires its own options.

## Using an Outgoing Relay

All other things being equal, sendmail is capable of delivering mail to any other MTA to which the sendmail program can connect. In most cases, this means that sendmail can deliver mail to any system on the Internet that runs its own SMTP server. It’s often desirable to configure a Linux computer to deliver mail directly, because this makes efficient use of network resources and bypasses a potentially unreliable mail relay. The Linux computer might *be* the official mail server, as well. There are, however, possible problems and limitations associated with sending mail directly. These include:

-   Unreachable destinations
    If the destination mail server is unavailable because it’s crashed or because of network problems, sendmail must hold the mail locally until the problem clears up. It must also periodically reattempt delivery. These actions consume CPU time, disk space, and network resources, although in all probability, very little of each. Of potentially greater importance, if the system that’s sending the mail has an intermittent Internet connection (such as a PPP link), subsequent send attempts may fail because that connection is down, thus resulting in a failure to deliver the mail at all, rather than a short delay.

-   Dial-up anti-spam configurations
    The *Dial-up User List (DUL)* is a list of IP addresses associated with dial-up (typically PPP) connections. (See http://www.mail-abuse.org/dul/ for more information on the DUL.) Many mail servers use the DUL, or similar lists maintained by others, to block mail from these connections, because spammer’s sometimes abuse dial-up lines to send spam. If your ISP has placed your dial-up number on the DUL, some recipients will reject your direct mail on this basis. Relaying your mail through the ISP’s official server will work around this problem; the DUL affects *only* e-mail that’s sent directly from a listed address.

-   ISP blocks of port 25
    Also in an effort to fight spam, some ISPs block outgoing connections from their dial-up addresses when directed at port 25 (the SMTP port) on remote systems. If your ISP does this, you won't be able to send mail directly at all; you *must* relay mail through your ISP's mail server.

-   Remote anti-spam measures
    Some mail servers take fairly extreme anti-spam measures, some of which may block your access attempts even if you're not hit by a DUL entry or by an ISP that blocks your port-25 access attempts. For instance, a remote site might block your e-mail if your claimed hostname doesn't match the hostname associated with your IP address, as would most likely be the case when you use a PPP account.

For all these reasons, it's generally a good idea to configure a dial-up Linux computer to relay mail through your ISP's mail server. On the other hand, some ISPs' mail servers are themselves notoriously unreliable, so you may prefer to brave the risks of sending mail directly. By contrast, if your computer is connected to the Internet in a more permanent fashion, relaying mail offers fewer advantages—but then, it also typically offers few or no *disadvantages* if your ISP or organization provides a mail server for this purpose. You may want to consult with your ISP or network administrator to learn more about the advantages and disadvantages on your particular network. Of course, you can also add your own personal experiences—if you know that your organization's mail server is unreliable, then sending mail directly can be quite desirable.

The default Red Hat configuration (and the default configurations for other distributions) sends mail directly. To change this configuration detail, you must add the following line to your sendmail.mc or equivalent m4 configuration file:

```
FEATURE(`nolixclient', `mail.example.net')
```

**Note** Options passed through the FEATURE command in sendmail.mc are often enclosed in single quotes. Unlike most configuration tools, though, m4 requires different opening and closing quotes. The opening quote is the back quote character, which is usually available on the key to the left of the 1 key on a keyboard. The closing quote is the usual single quote character, which is on the key to the right of the semicolon (;) key on most keyboards.  You should, of course, change mail.example.net to your organization's or ISP's mail relay system. When you've rebuilt sendmail.cf and restarted sendmail, the result should be that all mail sent through your local copy of sendmail is relayed through the mail relay system you specify.

**Tip** One objection that's frequently voiced to using an ISP's mail relay comes from users who use multiple ISPs. Because most ISPs reject mail relay attempts from outside their domains, a configuration like this will work from only one ISP. One way around this problem is to create *two* sendmail.cf files, one for each ISP. Name each one something appropriate, such as sendmail.cf.isp1 and sendmail.cf.isp2. You can then modify your PPP dial-up scripts (described in Chapter 11) to copy the customized files over the regular sendmail.cf and restart sendmail. The result is that sendmail will relay through whichever ISP's mail server is appropriate.

## Configuring Sendmail to Relay for a Domain

Configuring sendmail to use another mail server as a relay is convenient on small Linux systems that function as workstations. Linux is often used as the mail server that relays for others, however. This configuration works best when the Linux server has a dedicated connection to the Internet that is always up. By default, all modern Linux distributions are configured so that they don't relay mail from other systems. This is an anti-spam measure, but it gets in the way of the use of a Linux server as a relay for your own computers. The trick is to *loosen*, but *not remove*, the anti-relay restrictions.

**Note** To have sendmail function as a relay, it must also be configured to receive mail. You may need to tweak your configuration to allow this, as described in the section "Receiving Mail."

To allow sendmail to relay mail from certain classes of computers, you must add a FEATURE line to sendmail.mc or its equivalent file. This FEATURE line includes one of the following options:

-   *promiscuous_relay*
    This extremely dangerous option tells sendmail to relay any mail that comes its way. Don't use this option, because it virtually guarantees that spammers will, sooner or later, abuse your system.

-   *relay_based_on_MX*
    This option configures sendmail to accept relays from other computers, so long as those computers' domains are configured to show your system as the MX. This option is fairly lax on security, because it essentially lets somebody else (whoever controls the DNS server for the remote system) determine whether your system will function as a relay.

-   *relay_entire_domain*
    If you set this option, sendmail accepts mail from any host within the domain to which it belongs. This can be a convenient way to quickly configure a Linux system as a limited mail relay.

-   *relay_local_from*
    This option tells sendmail to accept relays if the sender uses the server's address as its own. This can be convenient in some cases, but it's also easily abused.

-   *relay_hosts_only*
    This option works with an access database (described shortly) to allow you to list individual hosts as acceptable or unacceptable for relaying.

-   *access_db*
    This feature allows you to use an access database (described shortly) to list domains for which sendmail will relay.

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

-   **OK** Forces sendmail to accept the mail, even if other rules would reject it.
-   **RELAY** Accepts for relay mail that comes from or goes to the specified domain.
