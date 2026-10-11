| Header | Purpose | 
| --- | --- | 
| DL-Expansion-History: | Provides data regarding the expansion of MTS distribution lists. This header is only used when you are dealing with having SMTP talk to an X.400 protocol. | 
| Path: (Usenet news header) | Specifies which news servers the post passed through. | 
| Received: (SMTP mail header) | Specifies which mail servers the mail passed through. | 
| Return-Path: | Specifies where a direct response to this email should go. |

Following the first line is a collection of Received headers, which are also part of the Trace Information header type:

```
Received: from thyme.spices.com (192.168.33.130 [192.168.33.130]) by
 davinci.inventors.com with SMTP (Microsoft Exchange Internet Mail Service
 Version 5.5.2650.21)
 id 1F5AK1W9; Wed, 8 Mar 2000 18:57:11 -0800
 Received: from cinnamon [192.168.1.301]
 by thyme.spices.com (8.9.1/8.9.0) with ESMTP id SAA02477
 for <dsmith@inventors.com>; Wed, 8 Mar 2000 18:53:19 -0800 (PST)
```

Every piece of email has one or more Received headers, each of which is a record of a mail server this email passed through, and when. You read these headers from bottom to top. In this case, the mail originated at the machine cinnamon on the network spices.com. This machine passed the mail to its mail server, thyme, using the Extended Simple Mail Transfer Protocol (ESMTP). The thyme.spices.com resolver looked at both the destination address and the MX record for the destination domain. It found in that MX record that the email server to contact was davinci.inventors.com, and so used SMTP to deliver the mail to the recipient’s mail server, which then delivered it to the recipient.

After this is the Message-Id header, which is one of the Message Identification and Referral header fields. A list of these fields is provided in Table 12.2.

Next in the message header is the unique identification value assigned to this particular piece of email:

```
Message-Id: <4.2.2.20000308184720.02166ef0@thyme.spices.com>
```

Following this unique ID value comes this line:

```
X-Sender: msmith@thyme.spices.com
```