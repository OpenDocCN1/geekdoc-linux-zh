If your version of Sendmail has STARTTLS support configured, it should appear as 250-STARTTLS when you execute the following command (note the third line from the bottom):

```
[ramon]$ telnet localhost 25
Trying 127.0.0.1...
Connected to localhost
Escape character is '^]'.
220 redhat.example.com ESMTP Sendmail 8.11.0/8.11.0; Sun, 26 Nov 2000
21:04:55 -0500
ehlo localhost
250-local.sendmail.COM Hello localhost [127.0.0.1], pleased to meet you
250-ENHANCEDSTATUSCODES
250-DSN
250-STARTTLS
250 HELP
quit
```

# ### Using STARTTLS

There are two useful applications for Sendmail's STARTTLS support:

+   - Allowing relaying based on successful certificate authentication
+   - Restricting SMTP connections to those who are valid certificate holders

By requesting a CA-signed X.509 certificate from all SMTP users requesting mail relaying, the local Sendmail agent can ensure that only authenticated users are allowed to relay through your server, regardless of what IP address they may be coming from.

In addition, STARTTLS can be used to allow SMTP connections to your mail server only in the event that the remote system has presented a valid certificate that can be verified by the local server's CA. You can either restrict incoming connections to those clients holding a valid certificate, or you can force outgoing mail connections to only succeed if the remote end can accept your certificate and agree to establish a secure (encrypted) SMTP session. You can use this last feature to set up a virtual private SMTP link over the public Internet, where you can share sensitive information via e-mail with a greater degree of confidentiality.