Date: Fri, 6 Jul 2001 13:55:36 +0100 (BST)
from: <vanderb@mydom.com>
to: <tayab@exsample.com>
subject: cat food

Are there any tins of Yum Yum in the fridge?

Eye, v.

We'll go through each of the commands and responses in the next module. First, let's look at the **tcpdump** traces. The normal trace below (edited to show only the start and end of the session) illustrates the three-way handshake (SYN, SYN-ACK, ACK) that establishes the connection, and the FIN, ACK, FIN, ACK termination that we covered in Module 10.9.

```
alice# tcpdump -t -N port 25 and host dave and alice
alice.1618 > dave.smtp: S 2242172728:2242172728(0) win 16060 <mss 1460,
dave.smtp > alice.1618: S 1486400000:1486400000(0) ack 2242172729 win 1
alice.1618 > dave.smtp: . ack 1 win 16060 (DF) [tos 0x10]


alice.1618 > dave.smtp: P 183:189(6) ack 298 win 16060 (DF) [tos 0x10]
dave.smtp > alice.1618: P 298:327(29) ack 189 win 4096
dave.smtp > alice.1618: F 327:327(0) ack 189 win 4096
alice 1618 > dave.smtp: . ack 328 win 16060 (DF) [tos 0x10]
alice 1618 > dave.smtp: P 189:189(0) ack 328 win 16060 (DF) [tos 0x10]
dave.smtp > alice.1618: . ack 190 win 4096
```

Below we see one line of the **tcpdump** ASCII dump, illustrating that the characters in the mail message are transmitted within the TCP packet “as is” – there's no magic encoding or clever tricks:

```
alice.1618 > dave.smtp: P 126:171(45) ack 254 win 16060 (DF) [tos 0x10]
0x0000 4510 0d5e 839e 4000 4006 03e5 d48c 8511 E.U.0.0.
0x0010 d48c 8505 0652 0019 854a d7b6 5898 safe ....R.......X...
0x0020 5018 3ebc 4715 0000 4172 6520 7468 6572 P.>G..Are.ther
0x0030 6520 616e 7920 7469 6e73 6e73 6520 5975 e.any.tings.Yu
0x0040 6d20 5975 6d20 696e 2074 6865 2066 7269 m.Yum.in.the.fri
0x0050 64 67 dg
```

Using **telnet** as an e-mail client in this way, to send a message, can be very useful:

+   - it helps us understand at a fundamental level how the mail system works
+   - a regular mail client may not be available, e.g. when you've just started installing a network, or are working on a non-destkop machine that doesn't have any mail clients but you need to troubleshooting the e-mail system, or are on a system that you are not familiar with or when you can't use a normal mail client because you don't have the necessary login codes
+   - it avoids the extra layers of configuration detail (and possible errors) that come with standard mail clients, so if you have a problem, **telnet** can help you isolate the cause: if **telnet** works and your client doesn't the problem is in the client.

In the next module we look at each of the SMTP commands we have used above.