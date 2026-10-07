One of the most useful things that the -bv option does is process the input address through the aliases database. The test of MAILER-DAEMON shows this. On this system MAILER-DAEMON is aliased to postmaster, which in turn is aliased to root. root is then aliased to craig. The address echoed back for the MAILER-DAEMON test is craig-the address after aliasing has been performed.

The last two tests are interesting because they show how -bv can be used to test a new configuration. In example, the client-only configuration file created in Chapter 9 using the nullclient feature is tested. The nullclient feature sends local mail to the MAIL_HUB server. The test of craig joe clearly shows this. In the first test, the default configuration, those addresses are delivered on the local host by the mailer. In the last two, those addresses are sent via the relay mailer to foobirds.org, which in this example is the MAIL_HUB server. The -bv test is a simple and useful tool for testing a relay client configuration.

The -C option is used in the last two -bv tests to test a new configuration. If -C is not used, sendmail uses the default sendmail.cf file. On Linux systems, the default sendmail.cf is found in either /etc or /etc/mail, depending on your configuration. -C to test a new configuration file before you make your default sendmail.cf configuration.

Another command-line option, like -bv, was used earlier in this book is -v. The -v option runs the sendmail command in verbose mode.

# Running in Verbose Mode

Verbose mode was used in Chapter 1, "Internet Mail Protocols," to display the SMTP protocol interactions between two systems exchanging e-mail. In Chapter 1, we ran the sendmail command with the -v option for verbose output and the -t option that we could type in the message from the terminal. It is not necessary to send a real message when you want to observe the protocol interactions. For that, an empty message works as well as a real message. Listing 10.2 shows the output of the sendmail command when it is run in verbose mode with an empty message.

+   10.2 Using Sendmail Probe

```
[root]# sendmail -v craig@wren.foobirds.org < /dev/null
craig@wren.foobirds.org... Connecting to wren.foobirds.org.
esmtp...
20 wren.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Tue,
31 Oct 2000 15:49:19 -0500
>>> EHLO ibis.foobirds.org
250-wren.foobirds.org Hello root@almond.nuts.com [172.16.12.1],
pleased to meet you
```