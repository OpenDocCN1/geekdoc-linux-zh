# Chapter 10 Testing Sendmail

250-ENHANCEDSTATCODES
250-EXPN
250-VERB
250-8BITMIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-AUTH DIGEST-MDS

>>> MAIL From:<root@ibis.foobirds.org...>
250 2.1.0 <root@ibis.foobirds.org...> Sender ok
>>> RCPT To:<craig@wren.foobirds.org...>
250 2.1.5 <craig@wren.foobirds.org...> Recipient ok
>>> DATA

354 Enter mail, end with ". on a line by itself
>>>
250 2.0.0 0eVKnjp00881 Message accepted for delivery
craig@wren.foobirds.org... Sent (0eVKnjp00881
Message accepted for delivery)
Closing connection to wren.foobirds.org.
>>> QUIT

221 2.0.0 wren.foobirds.org closing connection
Unlike Chapter 1, this the sendmail command is not run with the -t option. Instead, the address of the remote recipient is typed in the command line, and the contents of a file are provided to Sendmail to be used as the mail message. The recipient is craig@wren.foobirds.org and the file is the null device, /dev/null. Clearly, the null device will not provide any real content, so we are in sending an empty message. The sole purpose of this test is to observe the protocol interactions.

> TIP Don't send empty messages to other users just to test e-mail. To test your system, get a free e-mail account explicitly for this purpose and send the tests to yourself at that account. To test a remote system, make arrangements with the administrator of that system before you starting test mail.

Listing 10.2, of course, begs "Why do you want to look at the protocol interactions?" SMTP has been around for a very long time. It is a simple protocol. Everybody does it correctly. You're not looking for errors in the SMTP protocol. What you're