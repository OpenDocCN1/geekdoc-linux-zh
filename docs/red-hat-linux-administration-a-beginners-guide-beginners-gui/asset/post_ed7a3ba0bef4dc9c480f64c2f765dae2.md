
While a POP client that is kept online for long periods of time can be configured to poll the server occasionally for new mail, IMAP avoids this problem altogether. A client connected to an IMAP server can be notified directly of any new mail that arrives.

Just in case the basic status indicators of read/unread, answered, important, and so on, aren’t sufficient for your needs, IMAP allows user-defined Status flags. This means you can mark messages in ways that are uniquely meaningful to you and your needs.

IMAP can even support non–e-mail applications. For example, you may set up a documentation repository as an anonymous read-only IMAP folder. This could then be available to your entire company and accessed with any IMAP client.

When the client performs its initial handshake with the server, it negotiates which capabilities are supported by both machines, and which are not. This structure makes it easy to add optional features to IMAP gradually, without a major upheaval to the protocol. For example, during the initial handshake, clients and servers can negotiate support for start-TLS–style encrypted connections, something that was not in the original IMAP specification.

For those with pay-by-the-minute Internet connections, or other specialized circumstances that make POP’s “offline” mode seem attractive, IMAP offers a “disconnected” mode. In this mode, all new mail is copied down to the client for local processing. Deletions and status changes are kept recorded by the client, and synced back to the server next time you connect. While this trades off connection time for bandwidth usage, it will still maintain many of the other advantages of using IMAP, such as a centralized mail store accessible by multiple clients, or custom status flags.

## Ask the Expert

- **Q:** Wow! IMAP sounds so cool. Are there any issues to consider when installing all these features?
- **A:** Even though the IMAP specification supports a large set of features, you’re still dependent on these features being implemented in your server and client software. Not all client software supports all of the more esoteric or recently proposed features of the protocol. Some server or mailbox configurations can also limit the features available for use.

![](img/ec2066d370d3af1a767664d36aa7ddfe_450_0.png)

Even though IMAP often involves less bandwidth than blindly downloading everything, its download-as-you-go approach can make it seem more sluggish to former POP users that are used to a "hit the Get Mail button, go for coffee, then come back and read mail" approach. These users may be good candidates to start with “disconnected” mode.

## 14.2 Installing POP and IMAP on Red Hat

In order to install IMAP on Red Hat 8, look for the Mail Server option in the Servers section, either in the **redhat-config-packages** tool or during the initial install. If you’re reinstalling by hand, you’ll want the **imap-2001a** rpm. Now, if you want to install a POP server, look for the Mail Servers option in the **redhat-config-packages** tool, or install the **imap-2001a** rpm. No, really. That’s not a typo, the POP server also comes with the IMAP package. Both servers come as part of the University of Washington’s IMAP server package (<http://www.washington.edu/imap/>). This is actually somewhat of an advantage if you’re running both services on the same box, as we’ll see later.

### Configuring the POP and IMAP Servers

There is a file entitled **CONFIG** that comes with the UW IMAP distribution, and its contents begin with the following words: “The IMAP and POP3 servers are plug-and-play on standard UNIX systems. There is no special configuration needed. Please ignore all rumors to the effect that you need to create an IMAP configuration file.” The remainder of the **CONFIG** file goes on to describe some minor source code tweaks that are possible at compile time, all of which are well beyond the scope of this book. (Perhaps, this will start to make up for having to deal with Sendmail’s configuration in the last chapter.) So, now that you have your POP and IMAP servers configured, you probably want to make sure they start up when needed.

### Starting the POP and IMAP Servers

Once again, starting the POP and IMAP servers when they’re needed is the job of our old friend **xinitd**. As usual, you can adjust whether these services start in **xinitd** from the **redhat-config-services** tool (the Services option under the System Tools submenu). There are four entries in the GUI tool that are of interest to us: **imap**, **imaps**, **ipop3**, and **ipop2**. The **imap** entry, as you may have guessed, turns on the IMAP server. If you want to use **imap** wrapped in an encrypted SSL connection, then you'll want to enable the **imaps** option. POP version 3 is the newest and most used version of the POP protocol, and it can be enabled with the **pop3** selection. The remaining selection, **pop2**, refers to the much older version 2 of the POP protocol, and there is probably very little, if any, reason to turn it on.

![](img/ec2066d370d3af1a767664d36aa7ddfe_451_0.png)

If you're looking to enable these services by hand, you'll be looking for the corresponding service names in the `/etc/xinetd.d/` directory. For each of the four service entries you should find the corresponding xinetd file, and edit it. You'll want to change the `disable` directive to No for each service you want to have started. The resulting file should look similar to the following example:

```
# default: off
# description: The IMAP service allows remote users to access their mail \
# using an IMAP client with SSL support such as Netscape \
# Communicator or fetchmail.

service imaps
{
    disable = no
    socket_type       = stream
    wait              = no
    user              = root
    server            = /usr/sbin/imapd
    log_on_success += HOST DURATION
    log_on_failure += HOST
}
```

## 14.3 Reading Mail with Telnet

Each request to and response from the POP or IMAP server is in cleartext ASCII (not counting SSL enabled connections), which means it’s very easy for us to test the functionality of a POP or IMAP server using Telnet. (This is especially useful when you have users who claim that the “mail server is broken,” although the real problem is that they’re unfamiliar with the system.) Like SMTP servers, POP or IMAP servers can be controlled with a very short list of commands. To get a look at the most common commands, let’s walk through the process of connecting to a server, logging in, listing available messages, reading one, and then dropping the connection.

> **NOTE**
> We’ll use the *telnet* command to read mail only as a means of seeing the actual commands being sent to the server and the server’s responses. You’ll rarely want to do this in the real world. Once your [email client] has been set up, you can read your mail with a mail reader such as Evolution or Pine. Knowing the actual POP3 or IMAP commands is helpful, however, when you need to track down problems reported by your users. Often, it’s easier to use Telnet to check quickly whether the POP or IMAP server is responding than to try to use a real mail client—especially if you suspect the mail client has a bug!

### Reading POP Mail with Telnet

We begin by *telnet*ing to the POP3 server. The POP server listens for connections by default on port 110. From a command prompt, type (substituting your own values where applicable):

```
[root@redbox /root]# telnet pop3server.domain.com 110
```

The POP3 server responds as follows:

```
+OK POP3 pop3server.domain.com v2001.78rh server ready.
```

The server is now waiting for you to give it a command. (Don’t worry that you don’t see a prompt.) First, you want to log in, and then tell the server your login name via the **user** command:

```
user yourlogin
```

Here *yourlogin* is, of course, your login ID. The server responds with:

```
+OK User name accepted, password please
```

Now tell the server your password, using the **pass** command:

![](img/ec2066d370d3af1a767664d36aa7ddfe_453_0.png)

> The system will echo back your password, so don’t do this if you have people looking over your shoulder!

```
pass yourpassword
```

where *yourpassword* is your password. The server responds with:

```
+OK Mailbox open, X messages
```

where *X* represents the number of messages in your mailbox. You’re now logged in and can issue commands to read your mail.

Begin by listing the messages that are waiting, using the **list** command. Type:

```
list
```

and the server will list all the messages in your mailbox. The first column represents the message number, and the second column represents the size of the message. The response for my mailbox currently looks like this:

```
+OK Mailbox scan listing follows
1 644
2 2303
3 2334
4 1599
5 2558
.
```

Now let’s try to actually read a message, using the **retr** command. The only parameter that **retr** needs is the message number to read. We’ll start simple: To read message 1, type:

```
retr 1
```

The server responds with something like this:

```
+OK 644 octets
Return-Path: <michael@domain.com>
Delivered-To: michael@redbox.domain.com
Received: by redbox.domain.com (Postfix) with ESMTP id 2010D1ED3A
   for <michael@domain.com>; Mon, 28 Oct 2002 22:32:38 -0700
```
