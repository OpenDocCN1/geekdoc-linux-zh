# Observing SMTP with Verbose Mode

Using telnet to connect to the SMTP port is a useful way to get a feel for the SMTP protocol, and it can be a useful test technique when you want to completely bypass your local copy of Sendmail to test the responses of a remote Sendmail server. A user typing in SMTP commands approximates the exchange of protocol information based on a best guess of how the two systems will interact. In most cases, it is much better to sit back and observe the systems actually interacting. The -v (verbose) option of the sendmail command lets you do exactly that. Listing 1.2 a piece of mail being sent with verbose mode.

Listing 1.2 The Protocol as Displayed by Verbose Mode

```
[craig$ sendmail -v -t
To: craig@wren
From: craig@ani
Subject: Test
Please ignore this test.
^
craig@wren... Connecting to wren.foobirds.org. via esmtp...
220 wren.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Mon, 23 Oct 2000
11:32:-0400
>>> EHLO ani.foobirds.org
250-wren.foobirds.org Hello root@ani.foobirds.org [172.16.12.11],
pleased to meet you
250-ENHANCEDSTATUSCODES
250-EXPN
250-VERB
250-8BITIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250-AUTH DIGEST-MDS
250 HELP

>>> MAIL From:<craig@ani.foobirds.org> SIZE=73
250 <craig@ani.foobirds.org>... Sender ok
>>> RCPT To:<craig@wren.foobirds.org>
250 <craig@wren.foobirds.org>... Recipient ok
>>> DATA
```