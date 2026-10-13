# Using sendmail to see the SMTP transaction verbosely

You can also use sendmail to see how it delivers a message to the destination. For example, the -vt option in the following command tells sendmail to be verbose and scan for To:, From:, Cc:, and Bcc: headers in the input:

```
sendmail -vt
```

After you run the preceding command, it waits for user input. At this point, you can enter something like this:

```
To: kabir@integrationlogic.com
From: someone@somewhere.com
Subject: Testing sendmail

This is a test.
```

After you enter a short message, as shown here, press Ctrl+D to exit message entry mode. Sendmail then displays an SMTP transaction similar to the following:

```
kabir@integrationlogic.com... Connecting to mail.integrationlogic.com via esmtp...
220 wormhole.integrationlogic.com ESMTP Sendmail 8.9.3/8.9.3; Sun, 21 Feb 1999 19:57:00 -0500
>> EHLO picaso.nitec.com
250-wormhole.integrationlogic.com Hello picaso.nitec.com {206.171.50.50}, pleased to meet you
250-EXPN
250-VERB
250-8BITMIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
```