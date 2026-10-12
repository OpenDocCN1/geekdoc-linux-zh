# **11.8  Mail headers**

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
| --- | --- | --- | --- |
| 1 | DJW2KPC | 21:42:14 | – |
| 2 | 2k_exch.example.com | 21:42:15 | 0:01 |
| 3 | 2k_5.example.com | 21:49:57 | 7:42 |
| 4 | eagle.example.com | 21:51:05 | 1:08 |
| 5 | mgate (at uit.co.uk) | 21:53:29 | 2:24 |
| 6 | dave (at uit.co.uk) | – | – |

The hop times are unusually slow. It's not uncommon for us to send a message to someone when we're talking to them on the phone, and a few seconds later we hear the “beep beep” of their e-mail client and they say they have received our message. On the other hand, when problems occur and messages take hours or days to arrive, checking the headers and the hop