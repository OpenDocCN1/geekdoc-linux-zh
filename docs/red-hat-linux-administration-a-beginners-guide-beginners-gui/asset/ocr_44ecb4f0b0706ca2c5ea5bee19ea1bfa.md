Among other things, this indicates that there are five messages in this mailbox (EXISTS), that one of them is new since the last time we checked mail (RECENT), and that first unread message has the ID of **4** (UNSEEN 4). Now let's retrieve a message:

03 fetch 4 rfc822

Remember that IMAP allows for retrieving portions of a message, such as just the header, or just one of many MIME parts. As a result, there are a good number of options for the **fetch** command. For our purposes here, we’ve specified to fetch message **4** in **rfc822** format, because this will give us nearly all of the message, and it’s the closest thing to a human readable response from the available options.

```
* 4 FETCH (RFC822 (632) 
Return-Path: <michael@domain.com>
Delivered-To: michael@redbox.domain.com
Received: by redbox.domain.com (Postfix) with ESMTP id 2010D1ED3A
	 for <michael@domain.com>; Mon, 28 Oct 2002 22:32:38 -0700
To: michael@domain.com
From: "michael" <michael@redbox.domain.com>
Message-Id: <20021028055811.E5QCD1D017B @redbox.domain.com>
Subject: important message for you
Date: Mon, 28 Oct 2002 08:05:52 -0700 (PDT)
User-Agent: Gnus/5.090007 XEmacs/21.4 Linux/RedHat
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Status: RO

Act now! Don't delay. Time could be running out. As seen on TV.
FLAGS (\Seen))
03 OK FETCH completed
```

You’ll notice at the end, the server also lets you know that it has marked this message as having been seen. Finally we can log out.

```
04 logout
* BYE redbox.domain.com IMAP4rev1 server terminating connection
04 OK LOGOUT completed
```

This barely scratches the surface of what IMAP is capable of, but is should be sufficient to test that your server is actually working as expected.