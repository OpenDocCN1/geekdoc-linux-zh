
- Interrogate domain’s sendmail to obtain e-mail addresses. They can use the sendmail EXPN command with likely mail groups such as all and engineering.
- Use the sendmail VRFY command to guess accounts by specifying common first and last names.
- For sites that do not support EXPN or VRFY they can simply send e-mail to all the names that they otherwise would have fed to EXPN or VRFY and note the ones that do not “bounce.”

It is common for spammers to say send e-mail to remove_address to take off of their mailing list. In many cases this is just a ploy to get recipients to validate the e-mail guess was correct and will have the opposite effect. In other words, by sending e-mail to the remove_address list, you actually are adding your e-mail address to the spammer’s list.

- Bait FTP sites to get clients to supply their e-mail addresses as the password for an anonymous login.
- Trade names with other spammers and those selling lists of names.

Some ways to reduce spam are listed here:

- Disable the VRFY and EXPN sendmail commands, as discussed in “Sendmail Security Options” on page 127.
- Do not list more e-mail addresses on your Web site than you need to. Each additional-mail address listed will attract spam.
- Consider having your users not supply valid e-mail addresses if they post to Usenet news. Some people will “munge” their e-mail address when posting and include textual instructions on how to “unmunge.” One example might be

auser@pentacorp.comedy (remove “edy” to send email)

or

auser at pentacorp dot com

or

auser@pentacorp.gov (change “gov” to “com”)

The latter is effective because many spammers will not send to .gov sites as they do not want the FBI after them. Some spam address collectors are smart enough to get an address despite these tricks.
- If your ISP offers anti-spam filters use them.
- If your ISP enforces reasonable restrictions on outbound mail to control spam try to accept them. It is becoming common for ISPs to require their subscribers to route all e-mail through their sendmail ports where they do some validation on the specified source address. This is so that they do not harbor spammers. Some may have overly restrictive policies, however.
- Use the Realtime Blackhole List to automatically reject spam. This is discussed in 'Blocking Spam' on page 133.

### 3.2.6 Drop-Shipping Spam (Relaying Spam)

**DANGER LEVEL ☠ ☠**

Prior to Sendmail 8.9, any Sendmail program would happily accept e-mail from any system in the world and forward it to any other system in the world. This was great for spammers. They could send a single piece of e-mail to your system with 100 recipients on other systems and let your system use up its bandwidth and computrons sending out 100 e-mail messages. Further, because they would give a phony return address you would be blamed as the originator of spam.

Fortunately, as of 8.9, Sendmail will only accept e-mail where either the recipient or sender is within their domain unless relaying is enabled. Additionally, as of 8.9, Sendmail normally will not accept e-mail if the From: address has a domain that is not real. Unfortunately, Sendmail is not smart enough to verify that the claimed From: address matches the numeric IP connecting to sendmail.

### 3.2.7 Blocking Spam

**DANGER LEVEL ☠ ☠ ☠ ☠**

There is the Realtime Blackhole List that is run by the MAPS project at http://maps.vix.com/. They accept reports of spammers and add them to the list. It is hard to get off the list. Both the actual spammers and any site that spam is relayed through (due to sloppy configuration by the SysAdmin) is a good candidate for this list.

Add the line

```
FEATURE(`rbl`)
```

to the /etc/sendmail.mc file to enable the Realtime Blackhole List. Then cause this feature to take effect with the following shell commands:

```
m4 /etc/sendmail.mc > /etc/sendmail.cf
/etc/rc.d/init.d/sendmail restart
```

By configuring your sendmail to query this site as to whether each piece of e-mail is spam, you will greatly reduce spam.

### 3.2.8 Spoofing Spam Robots

Spammers are not content just to get e-mail addresses from mailing lists and News groups. Also some search everyone's Web pages looking for addresses. Those “@” characters give it away, as does mailto: in the document. Some sites have taken to using dynamic pages to create an infinite number of generated links with bogus e-mail addresses. This wastes the spammer's cycles and bandwidth, both on getting these bogus pages and on sending e-mail to fake addresses. I do not have more details on how to do this but I am sure you can figure out basically.

One such program for generating these pages with fake e-mail addresses is called wpoison. It is available from

```
www.novia.net/~doumakes/abuse/
```

This site has other anti-spam ideas including various filters. I hope that if anyone does this, they make the effort not to confuse “good” search engines such as altavista.com and google.com. The “good” search engines respect your asking them to avoid certain pages (such as the spam 'bot spoofing pages).

### 3.2.9 Allowing Controlled Relaying

![](img/7d04225c75a86d3cf4bd6077596f35b2_155_0.png)

There are several features to enable relaying without opening your mail server to spam attacks. To enable relaying from all hosts within your domain, add the following to /etc/sendmail.mc:

```
FEATURE('relay_entire_domain')
```

Then use this feature to take effect with the following shell commands:

```
m4 /etc/sendmail.mc > /etc/sendmail.cf
/etc/rc.d/init.d/sendmail restart
```

The /etc/mail/access file may be used to reject e-mail from specified sites and to allow mail from sites that would be rejected. After editing this file, issue the following commands to cause the changes to take effect:

```
makemap hash /etc/mail/access < /etc/mail/access
/etc/rc.d/init.d/sendmail restart
```

Each line of /etc/mail/access is an entry. The first field of each line is an address that you want to work with. It may be an e-mail address, a domain, a fully qualified host name, or part of an IP address. This field should be separated from the next with one or more spaces or tabs. The next field should be an instruction telling sendmail what to do with e-mail from this address. Valid values are listed in Table 3.2.

Table 3.2 /etc/mail/access Instructions

| Instruction | Meaning |
|---|---|
| OK | Accept e-mail unconditionally. |
| RELAY | Accept e-mail and allow relaying unconditionally. |
| REJECT | Reject e-mail with a standard rejection message. |
| DISCARD | Throw message away without bouncing back to sender. This feature only works for matching senders, not recipients. |

```
### text
### text must be an RFC 821-compliant error code.a.
text is the message to the sender.
```

a. RFC 821 is available at www.fao.org/rfc/rfc821.html.

As an example, you say want to reject e-mail from quickmoney@hotmail.com, any in the cracker.com domain, or in the 10.1.*. network. You want to say Spammer, go home to anyone at stocktips.com, but you will accept e-mail from friend.stocktips.com. Because you see spam from eternal_youth@ from a variety of hostnames, you want to reject it too. And you want to relay for pentacorp.com.

The following entries in /etc/mail/access would be needed:

```
quickmoney@hotmail.com REJECT
cracker.com             REJECT
10.1                     REJECT

friend.stocktips.com    OK
stocktips.com           550 Spammer, go home
etern_youth@            550 Spammer, go home

pentacorp.com           RELAY
```

Note that the difference between OK and RELAY is that OK allows that to send mail into your sites but RELAY also allows e-mail from that address to be sent out onto the Internet (relayed).

You can also blacklist recipients by adding the following line to /etc/sendmail.mc:

```
FEATURE(`blacklist_recipients`)
```

You will need to issue the following commands to enable this:

```
m4 /etc/sendmail.mc > /etc/sendmail.cf
/etc/rc.d/init.d/sendmail restart
```

The onclick_recipients feature is enabled, recipients may be black-listed. To reject e-mail addressed to account george, demo.pentacorp.com, and sal@lab.pentacorp.com, the following lines in /etc/mail/access will be:

```
george 550 George is on safari until February
demo.pentacorp.com 550 It is a demo system, get a life
sal@lab.pentacorp.com 550 We fired her
```

After changing /etc/mail/access, be sure to restart Sendmail thus:

```
/etc/rc.d/init.d/sendmail restart
```

### 3.2.10 Allowing POP and IMAP Clients to Send Mail

Dynamic relay authorization control (DRAC) interfaces with your POP or IMAP server to temporarily allow Mail Transfer Protocol (SMTP) relay access from client systems that have picked up mail from your network, typically in the last 30 minutes. This is reasonably because both POP and IMAP require an account and password. The "reasonably" is only because the SSL-wrapped versions of these (SPOP and SIMAP) encrypt the password before sending over the Internet. If one of the SSL-wrapped versions of mail download clients used (SPOP or SIMAP), then this arrangement would have good security as there is a small window of opportunity for someone else (e.g., whoever might get the dynamic IP address within 30 minutes of a client system transferring mail) to inject spam.

This is an elegant solution for traveling employees as it allows their e-mail to originate from your site and prevents them from spamming you from the same network or dynamic IP address. DRAC uses RPC to communicate between the POP/IMAP and SMTP servers. Since RPC is considered an insecure protocol, be sure to block access to RPC from other systems with IP Tables or IP Chains.

Information on DRAC and downloads are available from

```
http://mail.cc.umanitoba.ca/drac/index.html
```

### 3.2.11 Disallowing Open Mailing Lists

An open mailing list is defined as one where anyone can send mail to that mailing list and it will be forwarded to everyone on that list. Large open lists are discouraged because of the spam potential, especially where some of the recipients are outside the organization-maintaining.
