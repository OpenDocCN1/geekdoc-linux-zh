where **yourpassword** is your password. The server responds with

```
«OK yourlogin has X messages (Y octets)»
```

where **X** and **Y** will be actual numbers. **X** represents the number of messages in your mailbox, and **Y** represents the number of bytes in your mailbox. You’re now logged in and can issue commands to read your mail.

We begin by listing the messages that are waiting, using the **LIST** command. Type

# **LIST**

and the server will list all the messages in your mailbox. The first column represents the message number, and the second column represents the size of the message. The response for our mailbox currently looks like this:

```
«OK 5 messages (13040 octets)»
1 4246
2 2303
3 2334
4 1599
5 2558
```

Now let’s try to actually read a message, using the **RETR** command. The only parameter that RETR needs is the message number to read. We’ll start simple: To read message 1, we type

```
```
RETR 1
```
```

The server responds with something like this:

```
Return-Path: <bob@domain.com>
Received: from localhost (localhost [127.0.0.1])
        by ford.domain.com (8.9.3/8.9.3) with ESMTP id WA08271
        for <sahsha@localhost>; Wed, 23 Jun 1999 22:32:38 -0700
Received: from domain.com
        by localhost with POP3 (fetchmail-5.0.0)
Received: (from budel@localhost)
        by dehatstar.domain.com (8.9.2/8.8.7)  Wed, 23 Jun 1999 22:32:38 -0700 (PDT)
Received: for sahsha@localhost: (single-drop); Wed, 23 Jun 1999 08:05:52 -0700 (PDT)
From: “R. D. Core” <chd@cdehatstar.domain.com>
Message-Id: <199906231505.LAA06752@dehatstar.domain.com>
Subject: Always remember!...