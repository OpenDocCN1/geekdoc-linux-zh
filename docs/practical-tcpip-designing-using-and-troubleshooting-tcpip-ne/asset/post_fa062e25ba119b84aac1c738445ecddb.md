
## 11.8 Mail headers

We've seen that a mail message is handled by several SMTP servers – usually two at least – as it travels from sender to recipient. As the message passes through each server, an extra mail header is added to the message, giving information about this mail hop – which server handled the message and when. These headers are often useful when resolving problems. (We didn't show any of these extra headers in the example in Module 11.5 because most e-mail clients hide them by default, both to avoid cluttering the screen and so as not to confuse naive end-users.)

Below we show a message we received:

```
Received: from mgate (mgate [212.140.133.29]) by dave
(8.7.3/8.7.3/dave) with ESMTP id VAA13434 for <bex9@uit.co.uk>;
Sun, 17 Jun 2001 21:53:29 +0100 (BST)
Received: from eagle.example.com ([192.0.2.1]) by mgate
(Post.Office MTA v3.1.2 release (P0203-101c) ID# 0-0U10L2S100)
with ESMTP id AAA21148 for <bex9@uit.co.uk>;
Sun, 17 Jun 2001 21:51:05 +0100
Received: by eagle.example.com with SMTP
from 2k_5.example.com (pc248-126.example.com [192.0.2.126])
id VAA31012 for <bex9@uit.co.uk>; (3.2.1/3.1.37);
Sun, 17 Jun 2001 21:49:57 +0100
Received: FROM 2k_exch.example.com BY 2k_5.example.com ;
Sun Jun 17 21:42:15 2001 +0100
Received: from DJW2KPC ([10.1.1.16]) by 2k_exch.example.com
with Microsoft SMTPSVC(5.0.2195.2966);
Sun, 17 Jun 2001 21:42:14 +0100
Message-ID: <00201c0f76d8fde51a081001010a@example.com>
From: "John K. Langle" <jk1@oexample.com>
To: "Bill Knasthir" <bex9@uit.co.uk>
References: <1010613141718.2M4623@techpc>
Subject: Re: r14 upgrade
Date: Sun, 17 Jun 2001 21:42:14 +0100
```

This message passed through five machines at least, and the timestamps show how long it takes the message to travel over each hop:

| No. | Machine name | Forwarded message at | Hop duration |
| :--- | :--- | :--- | :--- |
| 1 | DJW2KPC | 21:42:14 | – |
| 2 | 2k_exch.example.com | 21:42:15 | 0:01 |
| 3 | 2k_5.example.com | 21:49:57 | 7:42 |
| 4 | eagle.example.com | 21:51:05 | 1:08 |
| 5 | mgate (at uit.co.uk) | 21:53:29 | 2:24 |
| 6 | dave (at uit.co.uk) | – | – |

The hop times are unusually slow. It's not uncommon for us to send a message to someone when we're talking to them on the phone, and a few seconds later we hear the “beep beep” of their e-mail client and they say they have received our message. On the other hand, when problems occur and messages take hours or days to arrive, checking the headers and the hop times can give you a pointer to where the problem lies. We've occasionally seen messages sent to us that have sat for hours on some virus-scanning or content-filtering machine on the sender's site, only to be released late at night (see Module 25.2).

Timestamps are often not very accurate because computer clocks often drift over time. (The clock on one of our server machines had drifted about 12 minutes in 10 weeks uptime.) It's a good idea to run NTP (Network Time Protocol – Module 17.13) to keep all your clocks in sync.

Most e-mail clients show only selected mail headers, to save space on the screen and to avoid confusing users who just want to read the content of their mail messages and not the gory details of every machine the message happened to pass through. When you *do* want to see all the headers, you choose specifically to display them. Figure 11.5 shows Outlook's display of the headers (select message > File > Properties > Internet).

![](img/a2132b646d336d5f9a21102d6320e537_330_0.png)

**Figure 11.5** Outlook's header displays

Figure 11.6 shows Outlook Express (select message > File > Properties > Details).

![](img/a2132b646d336d5f9a21102d6320e537_330_1.png)

**Figure 11.6** Outlook Express: select message

In Netscape, you set an option for the level of header detail to be displayed in the message windows using the menu View > Headers > All.

In the next module we explain how the client receives messages using POP.

## 11.9 POP3 clients and servers

POP3 is the “Post Office Protocol.” The name comes from the idea that my messages are stored in a mailbox somewhere (the POP server) and I need a mechanism to retrieve them, which I can do from any workstation on my network, in the same way that I might collect my snail-mail from an office of my country’s postal service. A significant element of the design is that all the mail messages for this site are delivered to the mailbox server (POP server) and not to individual users’ machines, because:

- a server machine is more likely to be available 24 hours/day, and not switched off at night like many client machines
- a central delivery point insulates external sites from the details of which workstation I happen to be using because messages are delivered to the POP server, my individual machine.

Figure 11.7 shows the message flow for a typical site. The incoming message is received by the SMTP server, *not* the POP server, although they may be on the same machine, and one software application may include both components. But that’s more a marketing or packaging issue: from a technical point of view, you need two separate components. (How the SMTP server passes the message to the POP server doesn’t concern us, and isn’t covered by any Internet standard – it’s up to the implementers of the particular applications.)

![](img/a2132b646d336d5f9a21102d6320e537_331_0.png)

**Figure 11.7** How a pop client receives a message

The POP server has three functions:

1. transfer messages, somehow, from the SMTP server (or servers) that receives the incoming e-mail for our users
2. manage the message store, inserting new messages, and extracting messages from it when users connect to this server to retrieve messages
3. handle the connections from clients and participate in the POP dialog, which we describe in the next module.

As with SMTP, the address of the POP server to use is part of the e-mail client's configuration. As the client connects to server using an IP address and the well-known POP port (:110), the POP server can be anywhere – it doesn't have to be on the local LAN. The configuration shown in Figure 11.8 is used by small sites that rely on their ISP to provide the mail servers. This is how most clients using single-user dial-up accounts collect their mail.

![](img/a2132b646d336d5f9a21102d6320e537_332_0.png)

**Figure 11.8** How dial-up PCs use POP

Like SMTP, POP uses TCP for its networking, and uses text commands and responses. This means we can use telnet as a POP client to interact with a POP server, which is what we do in the next module. We show two examples, using telnet from Alice to retrieve messages from our POP server on Dave. (As preparation, in advance we sent four messages to user fred.)

Server response lines that begin with +OK indicate that the last command you entered succeeded; if the command failed, the line begins with -ERR. For clarity, we indented the server responses and show commands in uppercase, although most servers will accept lowercase too. To save space, we've deleted a few blank lines and some of the mail headers from the received messages.

The second example gives more of a feel for how a real POP client works. It can delete messages from the server after they've been read, which is the way it's normally done. Or the client can leave them on the server, simply by not issuing the delete command. You may want this if you read your mail both with a POP client on your desktop, and with a Web mail system from outside your LAN: mail clients usually provide a configuration option like “Leave messages on server.” Particularly useful in this context is the LAST command, which gives the number of the message that you last retrieved; clients use this to “get only new messages” when they are using the “leave messages on server” option.

That's all a mail client does really. Having a purpose-built mail client is just a convenience. It does nothing network-wise that you can't do with telnet (but gosh, that would be tedious).
