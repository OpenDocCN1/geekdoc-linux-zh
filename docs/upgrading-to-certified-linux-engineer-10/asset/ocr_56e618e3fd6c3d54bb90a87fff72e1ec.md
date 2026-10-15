The email header should contain a line for amavisd.

```
geeko@da51:~> mail
mail version 11.25 7/29/05. Type ? for help.
"/var/spool/mail/geeko": 1 message 1 new
>N 1 jgoldman@digitalai Tue May 16 15:30 20/829 Test
>1
Message 1;
From jgoldman@digitalairlines.com Tue May 16 15:30:58 2006
X-Original-To: geeko@digitalairlines.com
Delivered-To: geeko@digitalairlines.com
Subject: Test
X-Virus-Scanned: amavisd-new at example.com
Date: Tue, 16 May 2006 15:30:58 -0400 (EDT)
From: jgoldman@digitalairlines.com
To: undisclosed-recipients;

Test
?
```

# Configure AMaViSd-new

On SUSE Linux Enterprise Server 10 you can configure AMaViSd-new by editing one of the following files:

+   - /etc/sysconfig/amavis
+   - /etc/amavisd.conf

# /etc/sysconfig/amavis

The configuration file /etc/sysconfig/amavis is only available on SUSE Linux products.

In this file there are only two parameters:

+   - **USE_AMAVIS**. If set to yes, Sendmail or Postfix are prepared to use AMaViSd-new.