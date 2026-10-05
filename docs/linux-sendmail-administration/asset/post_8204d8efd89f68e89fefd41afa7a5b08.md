
## Understanding E-Mail Architecture

The capabilities of the network protocols described in Chapter 1, “Internet Mail Protocols,” define the technical boundaries of the Internet mail architecture. The global scope of Internet mail makes it obvious that these protocols can create a flexible architecture supporting an enormous amount of e-mail traffic.

SMTP provides direct end-to-end mail delivery. This is one of its strengths. In Chapter 1, telnet was used to simulate an SMTP connection for the purpose of examining the protocol interactions. Another thing is connection-oriented TCP transport. Using TCP means that end-to-end mail delivery is guaranteed. The person at the remote end may not read your mail, you may accidentally address it to the wrong person, or the server may redirect your mail, but you can rely on the fact that your mail arrives intact.

Because of the direct delivery model, SMTP systems like Sendmail can provide immediate feedback about delivery. Everyone, at one time or another, has sent a message and gotten an immediate response saying that user-so-so does not have an account on the remote host to which the mail was directed. This immediate feedback is available because the local system connects directly to the remote host, delivers the mail to that host, and accepts responses back from that. If the response is an error, the error message is immediately returned to the sender.

## Chapter 2 Understanding E-Mail Architecture

Some other mail systems use store-and-forward protocols like UUCP and X.400 that move toward its destination one hop at a time, storing the complete message at each hop and forwarding it on to the next system. The message process proceeds in this manner, one hop at a time, until final delivery is made. With a system like UUCP, your server will communicate directly with hosts that are directly attached to your server. UUCP is a particularly good example of the store-and-forward model because the traditional UUCP bang address format clearly shows the path that the mail takes to its destination. In the UUCP bang address format, each host in the forwarding sequence is explicitly named and the last value in the address is the name of the user to whom the mail is addressed. Figure 2.1 uses UUCP and SMTP to illustrate both store-and-forward and direct mail systems.

### Figure 2.1 Direct delivery versus store-and-forward

![](img/b8082498451dba2bf0cf2907c85c4c83_52_0.png)

Direct delivery allows SMTP to deliver mail without relying on intermediate hosts. If the delivery fails, the local system knows it right away. It can inform the user that sent the mail or queue the mail for later delivery without reliance on remote systems. The disadvantage of direct delivery is that it requires both systems to be fully capable of handling mail. Sometimes that's not the case, particularly with small systems as PCs or mobile systems like laptops. These systems are usually shut down at the end of the day and are frequently offline. Mail directed from a remote host with a “cannot” error when the local system is turned off or is offline. To handle these cases, SMTP can simulate the store-and-forward model by delivering the message to a mail server instead of delivering it to the end system. The remote mail server is then responsible for moving the mail to the end system.

The Domain Name System (DNS) tells the SMTP server when mail needs to be routed to another server instead of the end system.

## The Role of DNS

All Internet connections depend on IP addresses. DNS is a distributed database system that maps hostnames to IP addresses. However, DNS can do much more than just map addresses. Address (A) database records are only part of the story. DNS running on Linux supports about 40 different database record types.

> NOTE Some knowledge of DNS is needed to fully understand e-mail architecture. However, this is not a book about DNS. If you need to run a DNS server, see DNS Server Administration by Craig Hunt (Sybex, 2000), part of the Craig Hunt Library.

DNS database records have the same basic format. For the purposes of this book, the format of DNS database records can be simplified to three basic fields:

- The name field contains the name of the object to which the record applies. Generally, this is a domain name or hostname.
- The type field contains the database record type. For example, an address record has a field that contains the letter A.
- The data field contains the data specific to the type of record. For example, an address record contains an IP address in the data field.

Of the fifty possible record types, only a handful are used to build real DNS databases. Of this handful of records, one of the most important is the Mail Exchange (MX) record. MX records tell Sendmail where to deliver. The name field of an MX record contains the hostname that appears in the e-mail address, and the data field contains the hostname of the server to which the mail should be delivered. Two MX records define the mail server might contain the following:

```
foobirds.org.      MX      10 wen.foobirds.org.
foobirds.org.      MX      20 parrot.foobirds.org.
```

The name field contains the domain foobirds.org., meaning that these records pertain to the entire domain. If mail is addressed to user@foobirds.org, the mail is directed to the mail exchangers defined by these records. This is a popular configuration, particularly when combined with the ability of the mail server to masquerade the hostname in outbound mail. Masquerading makes it look if the mail sent by the local user

## Chapter 2 Understanding E-Mail Architecture

came from user@domain, which creates a balanced addressing scheme for both inbound and outbound mail.

> **NOTE** See Chapter 9, "Special Configurations," for detailed information about masquerading.

The sample MX record says that wren was the mail server for foobirds.org with a preference of 10. The second MX record identifies parrot as a mail server for foobirds.org with a preference of 20. The lower preference number, the more preferred server is. The record with the preference of 10 is used before the record with the preference of 20, meaning wren is the preferred server for foobirds.org and parrot is the backup server. A backup mail exchange server is used only when the preferred server is down or offline. The backup server holds the mail and periodically attempts deliver to the preferred server. When the preferred server comes back online, the backup server sends the mail to the preferred server. At that point, the backup server's job is done. A backup exchange server deals directly with the recipient. Its only job is to get the mail to the preferred server.

The sample MX record redirects mail addressed to the domain foobirds.org, but they do not redirect mail to an individual host. If mail is addressed to jay@hawk.foobirds.org, it is delivered directly to hawk; it is not sent to a mail server. This is a very flexible configuration that permits people to use e-mail addresses of the form@domain when they like, or use direct delivery to an individual host when they want that.

Some systems are not capable of handling direct-delivery e-mail. An example is a Microsoft Windows system that doesn't run an SMTP mailer daemon. Mail addressed to such a system would not be successfully delivered, and worse, would be reported to you as a network error! To prevent this, MX records are generally assigned to these individual hosts to redirect mail to the hosts to a valid mail server. Here are two examples:

- puffin.foobirds.org MX 5 wen.foobirds.org.
- robin.foobirds.org MX 5 wen.foobirds.org.

These records redirect mail addressed to puffin or robin to wren. In both cases, only one mail server is named for each host. With these records, mail addressed to daniel@puffin.foobirds.org is delivered to daniel@wren.foobirds.org. Sendmail does not need to select a server. All the mail goes to wren. The next section examines how Sendmail uses the DNS responses.
