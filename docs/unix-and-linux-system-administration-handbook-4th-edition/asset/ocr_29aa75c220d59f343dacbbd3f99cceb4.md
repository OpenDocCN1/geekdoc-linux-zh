You will need to put a properly signed certificate in /etc/certs/smtp.pem. It's also a good idea to turn on encryption on outgoing SMTP connections:

```
smtp_tls_security_level = may
smtp_tls_loglevel = 1
```

# Fighting spam and viruses

Postfix has many features that can help block suspicious email.

One class of protection features calls for strict implementation of the SMTP protocol. Legitimate mail servers should respect the protocol, but spam and virus senders often play fast and loose with it, thus giving themselves away. Unfortunately, broken mailers handling legitimate mail are still out there, so this technique isn't quite foolproof. Choose restrictions carefully, and monitor the log files.

Here are some of the main features in this category:

+   - reject_non_fqdn = * – rejects messages without a fully qualified sender domain (sender), recipient domain, (recipient) or HELO/EHLO hostname (hostname)

+   - reject_unauth_pipelining – aborts the session if the client doesn't wait to see the status of a command before proceeding.

+   - reject_unknown_sender_domain – rejects messages with an unresolvable sender domain. Postfix returns a temporary error message because the problem may result from a transient DNS glitch.

+   - reject_unknown_reverse_client_hostname – rejects messages from hosts that have no reverse DNS record.

+   - smtpd_helo_required – requires HELO/EHLO at the start of the conversation (parameter, either yes or no).

+   - strict_rfc821_envelopes – requires correct syntax for email addresses in the MAIL FROM and RCPT TO commands (parameter, yes or no).

The items above that are not marked as parameters are restrictions. You invoke them by including their names in smtpd_helo_restrictions (reject_non_fqdn_*) or smtpd_client_restrictions (the others). To test a restriction before putting it in production (always a good idea), insert the restriction warn_if_reject in front of it to convert the effect from outright rejection to warning log messages.

# Blacklists

You can tell Postfix to check incoming email against a DNS-based blacklist; see User or site blacklisting on page 792 for more details. To enable this behavior, use the reject_rbl_client restriction followed by address of the DNS server to be consulted. A similar feature is reject_rhsbl_sender, which checks the domain name of the sender's address rather than the client's hostname.