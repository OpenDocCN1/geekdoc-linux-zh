The fetchmail program allows an Ubuntu server with limited network capability (such as a dial-up connection) to contact the remote ISP server using either POP3 or IMAP as a normal email client and download any messages stored on the ISP server to the local system.

This means that instead of having multiple individuals connect to the ISP to download their messages, a small organization can run an Ubuntu server and configure fetchmail to download all of their messages at once and place them in local mailboxes on the server. The fetchmail software can redistribute individual messages for employees to the appropriate mailboxes on the Ubuntu server. Once the messages are on the local mailboxes, employees can connect to the Ubuntu server using their desktop email client package and retrieve their messages. For companies that don’t have a full-time Internet connection, fetchmail can be a cost-effective solution.

> The Ubuntu server’s email server installation doesn’t include the fetchmail program by default, but it’s easy to install. Just use the apt-get program to install fetchmail:
> 
> `sudo apt get install fetchmail`
> 
> For more information about configuring and using the fetchmail program, check out the main fetchmail web site at http://fetchmail.berlios.de.

```
sudo apt get install fetchmail
```

# Postfix Setup

The Postfix system consists of several mail queue directories and executable programs, all interacting with each other to provide mail service. Figure 23-3 shows a block diagram of the core Postfix parts.

![](bbox=[0.22, 0.87, 0.75, 0.98])

Figure 23-3: Block diagram of Postfix.