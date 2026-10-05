# ACLs (access control lists) 817

The next accept stanza guarantees mail to postmaster will always get through if it's sent to a local domain; this can help with debugging.

The require line checks if a bounce message can be returned, but it checks only the sender's domain.\ If the sender's username is forged, a bounce message could still fail (that, the bounce itself could bounce). You can add more checking by calling another program, but some sites consider such-calls abusive and might add your mail server to a blacklist or bad-reputation list.

The next accept stanza checks for hosts that are allowed to relay through it, namely local hosts that are submitting mail into the system. The control line specifies that exist as a mail submission agent and fix up any header deficiencies as the message arrives from the user agent. The sender's address is not checked because many user agents get confused by error returns. (This is appropriate for local machines relaying to a smart host, not for external domains that you might be willing to relay for.) DKIM verification is disabled because these messages are outbound from your users or relay friends.

The last accept stanza deals with local hosts that authenticate via SMTP AUTH. Once again, these messages are treated as transmissions from user agents.

We next check the domain to which the message is headed and whether it is in our list of local_domains or in our list of domains to which we allow relay, relay_to_domains.(These domain lists are defined anywhere.) Any destinations not in one of those lists are refused with the specified error message. DKIM verification is again disabled.

Finally, when all previous requirements have been met but no-specific accept or deny has been triggered, we verify the recipient and accept the message. Internet messages to local users fall into this category.

We haven't included any blacklist scanning in the example above. To access a blacklist, use one of the examples in the default config file or something like this:

```
deny condition = {$if ip4($sender_host_address)}
authenticated = *
hosts = +my_whitelist_ips
dnslist = list.dnswl.org
domains = +local_domains
verify = recipient
message = You are on R $dnslist_domain: $dnslist_text
dnslist = zen.spamhaus.org
logwrite = Blacklisted sender {$sender_host_address} \
$dnslist_domain: $dnslist_text
```

Translated to English, this code specifies that if a message matches all of the following criteria, it is rejected with a custom error message and logged (also with a custom message).

+   1. require means "deny if not matched."

![](bbox=[0.963, 0.233, 0.993, 0.353])