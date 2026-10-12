sends a "bounce message" to the originator of the original message saying it can't be sent. Some small companies only publish a single MX record for their sites. However, because the DNS allows backup SMTP servers to be specified for a domain as explained in the previous module, not being able to find *any* server to send to is relatively rare unless the problem is with your own Internet connection.

+   2. **the DNS has no MX records for the destination domain**
+   
+   If your server gets no MX records in response to its lookup, it then does an IP address lookup (not an MX lookup) on the domain name itself, to see if it is a *hostname*. If it's not a valid hostname, the server gives up and says it can't send the message.
+   
+   If it is a valid host, the sending server tries to connect to an SMTP server on the host's IP address, with the usual cycle of retries.
+   
+   This behavior is a carry-over from the pre-MX days, when e-mail was addressed to a specific machine – often the recipient's own machine – rather than just to the domain name. As we explain below, addressing messages to a specific machine within a domain can cause problems.

# # Some background to the concept of MX records

Originally, to send mail to someone you had to know the address of their individual machine, e.g. `fred@pc29.sales.example.com`. In a small community that was fine, but as the Internet grew, the concept of MX records evolved. By including only the site's domain name in an e-mail address, rather than the FQDN of a machine, we hide details of where a person is located within our organization. They can move to a different geographical office or change department or use a different desktop PC and their e-mail is still routed in correctly. People outside our organization are insulated from changes inside.

The MX record mechanism has other advantages: we can easily specify multiple e-mail servers for our domain, and it's possible for third-party service providers to handle e-mail for their customers, e.g. small sites rely on their ISP's mail servers and don't have to run their own.

# # MX records for subdomains

As we've seen, the destination server is located by querying the DNS for MX records for the part of the e-mail address following the `"@"`, which may in fact be a subdomain of a site's primary domain, as in `fred@asia.example.com`. If the subdomain is delegated, the DNS can contain MX records for it, allowing you to have mail for your main domain sent to one set of servers, and for the subdomain to a different set. Because this configuration limits user e-mail named to specific subdomains, it's most useful where the subdomain is organizationally very separate from the parent, e.g. a separate division covering a distinct geographical region.

Now that we know how to find the destination mail server, we explain how to send a message to it in the next module.