# DKIM Configuration

expn.com have been in the queue longer than 1,280 minutes. All the destinations in this example are suggestive of messages having been sent from vacation scripts in response to spam.

qshape can also summarize by sender domain with the -s flag.

# Soft-bouncing

If soft_bounce is set to yes, Postfix sends temporary error messages whenever it would normally send permanent error messages such as "user unknown" or "relaying denied." This is a great testing feature; it monitors the disposition of messages after a configuration change without permanently losing email. Anything you reject will eventually come back for another. Don't forget to turn off this feature when you are testing or you will have to deal with every rejected message over and again.

# Testing access control

The easiest to test access control restrictions is to send a message from an outside host and see what happens. This is a good basic test, but it doesn't cover special conditions such as mail from a domain where you have no login.

Postfix 2.1 introduced an extension to the SMTP protocol XCLIENT which simulates submissions from another place. This feature is disabled by default, but with the following configuration line in main.cf, you can enable it for connections originating from localhost:

```
smtpd_authorized_xclient_hosts = localhost
```

A testing session might look something like this:

```
$ telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'.
220 tardis.ee.ethch SMTP Postfix
XCLIENT NAME=mail.colorado.edu ADDR=192.168.131
250 Ok
HELO mail.colorado.edu
MAIL FROM: <evi@colorado.edu>
250 Ok
RCPT TO: <david@colorado.edu>
554 <david@colorado.edu>: Relay access denied
```

# 20.16 DKIM CONFIGURATION

Our DKIM coverage is a bit scattered. The introductory material is in the DNS chapter (on page 591) and on page 768 of this chapter. Here we concentrate on the email-related details of using DKIM through an external tool, amavisid, and directly, in conjunction with sendmail, Exim, and Postfix. sendmail and Postfix use

![](bbox=[0.955, 0.227, 0.995, 0.367])