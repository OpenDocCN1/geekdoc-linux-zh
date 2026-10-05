The access database shown in Listing 6.8 illustrates the various action field values are used.

# 6.8 Specifying Different Actions in the access Database

```
wespamu.com         REJECT
172.18               DISCARD
weselljunk.com      550 Junk mail is not accepted
wepushorn.com        ERROR:5.7.1:550 Relaying denied to spammers
riendly.org         OK
129.6               RELAY
```

The REJECT command causes Sendmail to return a standard error message to the source and discard the mail. The DISCARD command drops the mail without sending any message back to the source. Most anti-spam authorities discourage discarding mail because it does not discourage the spammer, knows you received the mail, so they just keeping some junk.

```
wepushorn.com         550 5.7.1 Relaying denied to spammers
```

The OK command causes Sendmail in Listing 6.8 to accept mail from friendly.org regardless of other conditions. For example, if mail arrives from a hostname that the friendly.org domain and cannot be resolved by DNS, Sendmail accepts that even though the accept_unresolvable_domain feature has not been enabled. To allow this you, of course, fully trust friendly.org.

The RELAY command causes Sendmail to relay mail for network 129.6 if basic relaying is not enabled on the system. Like the OK command, using the RELAY command means that you fully trust every host on network 129.6.