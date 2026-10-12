# ### 11.3 MX records for resilience

We want e-mail to be as reliable as possible. Making the user re-send messages just because our Internet connection was down for a while, or because the recipient’s server was being rebooted, is irritating at best and can lead to lost or forgotten messages. The DNS helps over-come this problem by letting you specify multiple SMTP servers for a domain. Here’s an example: below we see that the DNS for example.com says that five SMTP servers know about this domain and will accept mail for its users:

```
alice% host -t mx example.com

example.com   MX    10    msrv1.example.com
example.com   MX    10    msrv2.example.com
example.com   MX    20    mailgate.uit.co.uk
example.com   MX    50    relay1.theirisp.com
example.com   MX    70    burelay.theirisp.com
```

This example illustrates two important features of how MX records are used.

# #### 1. MX preference values for multiple servers

The third column above is the preference value: the smaller the value, the more preferred this entry is. Thus, our server will first try to contact **msrv1.example.com**. If that isn’t available it will move on to try **msrv2.example.com**, and so on. This is how you specify which are your “main” or preferred servers, and which servers are backups to be used when your main server(s) are unavailable.

If more than one address has the same preference value, your SMTP server will (or ought to) try them in random order. As soon as it successfully connects to one, it sends the message and that’s that. It only tries the later servers in the list if it can’t access the earlier ones. Trying the servers in random order spreads the incoming message load evenly across all the same-preference-value servers. But even if sending servers always choose the first server in the returned MX listing, there is another mechanism that gives a form of load-balancing. The DNS server involved here, i.e. for the recipient’s domain, doesn’t return the list of MX records in the same order every time. Instead, it round-robins them in successive DNS responses, so that each entry gets an equal number of turns at being top in the list. The result is that each successive incoming message will go to a different server. In the example above, **msrv1** and **msrv2** will each receive about the same number of messages. This is a common arrangement at large sites, for handling large messages volumes (by adding extra servers as needed) and for redundancy: if the first server tried is down, the message will be sent to the next server in the list.

You can see this round-robin effect easily by looking up the MX records for cus.cam.ac.uk a few times, and observing how the order of the entries changes: