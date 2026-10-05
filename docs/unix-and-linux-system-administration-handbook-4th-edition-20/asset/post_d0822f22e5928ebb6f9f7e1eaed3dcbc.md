
# Chapter 20

# Electronic Mail

## Content filtering

Postfix can use regular expressions to check the headers and bodies of messages for contraband. It can also pass messages to other programs such as spam fighting tools or antivirus applications.

Header and body checks are performed in real time as messages are accepted through SMTP. Each regular expression that is checked invokes an action specified in Table 20.25 on page 83 if the regex matches. For example, the line

```
header_checks = regexp/etc/postfix/header_checks
```

in main.cf with the following line in /etc/postfix/header_checks

```
/Subject: reject-me; REJECT You asked for
```

would reject any message whose subject contains "reject-me". Though regular expression support is always nice, it comes with caveats in the context of email processing. In particular, this is not an effective method of spam or virus filtering.

## Content filtering with amavisd

Industrial-strength virus filtering is usually implemented through amavisd (see page 769), a Perl program that interfaces mail server software with one or more antivirus applications. Such filters are configured with Postfix's content_filter parameter, which instructs Postfix to pass every incoming message once through the specified service. In addition to setting the content_filter parameter, you may modify some entries in the master.cf file and add new ones.

Postfix and amavisd interact with each other by means of the SMTP and LMTP protocols. Postfix sends the mail to be analyzed by amavisd through a port that is accessible only on the local machine and has content-scanning disabled (amavisd scans and sends it back to Postfix through SMTP at an alternative port (avoiding a loop)).

For mail coming from the Internet, amavisd typically listens on port 10,024, and Postfix's back-door port is often 10025. If we also process outgoing mail and want to differentiate from incoming mail, we need a separate amavisd port for—say, 10,026. The incoming mail can return to Postfix on the same return port as outgoing mail.

The configuration outlined below is a "post queue" that scans mail after it has been accepted into Postfix's queue. If you want to implement an in-scan setup, where the mail is scanned by the client's initial SMTP dialog, try the amavisd-milter helper tool, which lets connect Postfix to amavisd as a milter.

On the amavisd side, make sure that amavisd's configuration contains the following lines (This configuration uses separate ports for inbound and outbound messages):

```
$inet_socket_port = [10024,10026];
$notify_method = 'smtp:[127.0.0.1]:1025';
$forward_method = 'smtp:[127.0.0.1]:1025';
$interface['10024'] = 'INBOUND';
$interface['10026'] = 'OUTBOUND';
$policy_bank['ORIGINATING'] = 'ORIGINATING';
$policy_class['ORIGINATING'] = { 1, # indicates client is ours
```

You need to configure Postfix to send the mail to amavisd.
The README file in the amavisd-new distribution includes over 20 lines of boilerplate configuration you can put into /etc/postfix/master.cf to make amavisd accessible and able to send mail back to Postfix. Don't duplicate it; just use and refer to the README.

To tell Postfix to send mail to amavisd for scanning, add this line to main.cf:

```
content_filter = amavisd:[127.0.0.1]:1024
```

For differentiating incoming and outgoing mail, the configuration is a bit complicated. Instead of just the above directive, you need to modify smtpd_recipient_restrictions like this (in bold):

```
smtpd_recipient_restrictions =
  reject_unknown_sender_domain
  reject_fqdn_recipient
  check_sender_access regexp:/etc/postfix/tag_as_originating.re
  permit sasl_authenticated
  check_sender_access regexp:/etc/postfix/tag_as_foreign.re
  check_client_access hash:/etc/postfix/relaying_access
  reject_unauth_destination
  reject_unauth_pipelining
  reject_unknown_reverse_hostname
  reject_tbl_client spamhaus.org
  permit
```

Then put the following line in the file tag_as_originating.re:

```
FILTER = amavisd:[127.0.0.1]:1026
```

And in tag_as_foreign.re:

```
FILTER = amavisd:[127.0.0.1]:1024
```

Mail from external hosts matches the tag_as_foreign.re, which instructs Postfix to filter the mail by sending it to port 1024. All mail matches the tag_as_originating.re, but for external hosts it is replaced by the foreign tag.

## Debugging

When you have a problem with Postfix, first check the log files. The answers to your questions are most likely there; it’s just a question of finding them. Every Postfix program normally uses a log entry for every message it processes, the trail of an outbound message might look like this:

```
Aug 18 22:41:33 postfix/pickup: 0E4A93688: uid=506 from=<dws@ee.ethz.ch>
Aug 18 22:41:33 postfix/cleanup: 0E4A93688: message-id=<200401820412.GA11444@ee.ethz.ch>
Aug 18 22:41:33 postfix/qmgr: 0E4A93688: from=<dws@ee.ethz.ch>, size=577,nrc=1 (queue)
Aug 18 22:41:33 postfix/smtp: 0E4A93688: to=evi@ee.ethz.ch,relay-tids=ee.ethz.ch[129.132.2.217],delay=0 status=250 (Ok: queue is 54DD90B)
Aug 18 22:41:33 postfix/qmgr: 0E4A93688: removed
```

As you can see, the interesting information is spread over many lines. The identifier 0E4A93688 is common to every line: Postfix assigns a queue ID as soon as a message enters the mail system and never changes it. Therefore, searching the logs for the history of a message, first concentrate on determining the message’s queue ID. Once you know that, it is to grep the logs for all the relevant entries.

Postfix is good at logging helpful messages about problems that it notices. However, it’s sometimes difficult to spot the important lines among the thousands of normal status messages. This is a good place to consider using some of the tools discussed in the section Condensing log files to useful information, which starts on page 358.

## Looking at the queue

Another place to look for problems is the mail queue. In the sendmail system, a mailq command presents the contents of a queue. You can use it to see why a message has become stuck.

Another helpful tool is the qshape script that has shipped with recent Postfix versions. It shows summary statistics about the contents of a queue. The output looks like this:

```
$ qshape deferred
             T 5 10 20 40 80 160 320 640 1280
TOTAL 78 0 0 7 1 2 0 0
expn.com 34 0 0 0 0 0 0 0
chinabank.pb 5 0 0 0 0 0 0 0
```

qshape summarizes the queue (here, the deferred queue), sorted by recipient. The columns report the number of messages in the queue longer than 1,280 minutes.

## Soft-bouncing

If soft_bounce is set to yes, Postfix sends temporary error messages whenever it would normally send permanent messages such as "user unknown" or "relaying denied." This is a great testing feature; it monitors the disposition of messages after a configuration change without permanently losing email. Anything you reject will eventually come back. Don't forget to turn off this feature when you are testing or you will have to deal with rejected message over and again.

## Testing access control

The easiest to test access control is to send a message from an outside host and see what happens. This is a good basic test, but it doesn't cover special conditions such as mail from a domain where you have no login.

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

## 20.16 DKIM CONFIGURATION

Our DKIM coverage is a bit scattered. The introductory material is in the DNS chapter (on page 591) and on page 768 of this chapter. Here we concentrate on the email-related details of using DKIM through an external tool, amavisid, and directly, in conjunction with sendmail, Exim, and Postfix. sendmail and Postfix use

![](img/579efec8c67772f31ecf34844bbb71a2_893_0.png)
