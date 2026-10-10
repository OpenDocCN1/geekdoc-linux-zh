# Chapter 7  \*\*Why Didn’t My Email Go Through? Tracing Email Problems\*\*

Here are the full contents of the email:

```
Delivered-To: you@gmail.com
Received: by 10.182.250.51 with SMTP id yz19csp530770bc;
\ \ Wed, 11 Apr 2012 19:55:45 -0700 (PDT)
Received: by 10.42.179.196 with SMTP id br4mr523278lcb.42.1334199345873;
\ \ Wed, 11 Apr 2012 19:55:45 -0700 (PDT)
Return-Path: <greenfly@example.net>
Received: from mail.example.net (mail.example.net. [64.142.5.5])
\ \ by mx.google.com with ESMTPS id s4s1195712514gb.48.2012.04.11.19.55.44
\ \ (version=TLSv1/SSLv3 cipher=OTHER)
\ \ Wed, 11 Apr 2012 19:55:44 -0700 (PDT)
Received-SPF: pass (google.com: best guess record for domain of greenfly@example.net
\ \ designates 64.142.5.5 as permitted sender) client-ip=64.142.5.5;
Authentication-Results: mx.google.com; spf=pass (google.com: best guess record for domain
\ \ of greenfly@example.net designates 64.142.5.5 as permitted sender) smtp.mail=greenfly@
\ \ example.net
Received: by mail.example.net (Postfix, from userid 1000)
\ \ id 7FS62S4A3; Wed, 11 Apr 2012 19:55:43 -0700 (PDT)
Date: Wed, 11 Apr 2012 19:55:43 -0700
From: Kyle Rankin <ky@eexample.net>
To: you@gmail.com
Subject: Test Subject
Message-ID: <20120412025543.QD23360@example.net>
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Disposition: inline
User-Agent: Mutt/1.5.20 (2009-06-14)
```

Test Body

As you can see, a lot of extra information is in the email that you normally don’t see, and the bulk of the extra headers are like a postmark on an envelope. Each mail server the email goes through to get to its destination, starting with the initial mail server, leaves a Received header with a date stamp and information about the message. The next mail server in the list adds its header to the top of the message, and so on, so that the header you see at the very top of the message is actually the last mail server that ultimately received the message:

```
Received: by 10.182.250.51 with SMTP id yz19csp530770bc;
\ \ Wed, 11 Apr 2012 19:55:45 -0700 (PDT)
```