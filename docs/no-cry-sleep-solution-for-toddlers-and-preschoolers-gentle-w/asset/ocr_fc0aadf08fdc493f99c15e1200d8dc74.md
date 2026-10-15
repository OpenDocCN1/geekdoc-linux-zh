In the sendmail.mc file located on the host that you want to have handle the relaying of messages, you need to also add the following line:

```
FEATURE(relay_entire_domain)dnl
```

Run the m4 operation to install the changed configuration and then restart the server with the service operation, as described earlier.

You can now e-mail messages from one user to another across your network. For example, george@turtle.mytrek.com can now e-mail a message to larisa@rabbit.mytrek.com. The local Sendmail servers will take care of sending and delivering mail both to users within their hosts and those located on other network hosts.

# Configuring Sendmail for a Centralized Mail Server

Alternatively, you could set up a central mail server to handle all the mail on your network. Mail clients on various hosts could send their messages to the central mail server, which would then relay them out to the larger network or Internet. Mail could then be received at the central mail server, where clients could later retrieve it. There are several ways to set up a central mail server. One of the simplest is to run a central mail server on your gateway host, and then have null client versions of the Sendmail server running on local hosts. Any mail sent from local hosts would be automatically forwarded to the central mail server. Received mail could only be delivered to the central server, usually to a POP or IMAP server also running on the central server’s host. Users could then access the POP server to retrieve their mail.

For a centralized configuration, it would make sense to treat users as having their network domain as their address, rather than separate hosts in their network. So the user cece on rabbit.mytrek.com would use the mail address cece@mytrek.com, not cece@rabbit.mytrek.com. Users could have the same name as those on their respective hosts, and corresponding users would be set up on the gateway host to handle received mail managed by the POP or IMAP servers.

An effective simple mail server would involve several components:

+   - A central mail server running on the gateway host

+   - Each client running Sendmail as a null client

+   - Masquerading all mail to use the domain address only, not host addresses

+   - A POP or IMAP server running on the gateway host to handle received mail

# Configuring a Workstation with Direct ISP Connection

If you are running a Linux system that is not part of a network but does have a direct connection to the Internet through an ISP (Internet service provider), you could simply use the ISP mail servers for sending and receiving mail. Normally, you would have an SMTP mail server for outgoing mail and a POP server for incoming mail. However, you can also configure Sendmail to interface with your ISP.

Be sure to first comment out the DAEMON_OPTIONS option as shown in the previous sections.