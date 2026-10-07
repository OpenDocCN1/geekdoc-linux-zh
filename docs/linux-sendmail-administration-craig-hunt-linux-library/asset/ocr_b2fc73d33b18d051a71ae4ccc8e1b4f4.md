# Processing MX Records

When Sendmail has mail to deliver, queries DNS for the MX records for the hostname in the e-mail address. It sorts those MX records by preference number. Thus, the lower preference number, the earlier in the list a server appears, which makes servers with lower preference preferable to servers with high preference numbers.

Sendmail tries to deliver the mail to each mail server in order. It stops processing the list if it finds a server that will accept the mail or if it finds its own hostname in the mail exchange server list. If it cannot deliver the mail to any of the servers, it will use the address of the host and attempt to deliver directly to that host.

NOTE The process of first querying for MX records and then for address records is an idealized process described in RFC 974 (“Mail Routing and the Domain System”). In reality, Sendmail uses the DNS ANY query to get all and records about a host. That one query retrieves the MX records and the A records.

A backup mail exchange server determines how to deliver mail just like any other server by querying DNS for a list of MX records. However, it cannot send the mail to each server in turn in the MX list because, in the hands of an MX server, MX records have the potential to create mail-routing loops.

Assume that we have three MX servers in this order of preference: wren, parrot, and jay. when wren is down the mail is delivered to parrot, parrot fetches the MX records and attempts to deliver the mail to wren. wren is still down. parrot would queue the mail and not attempt to deliver it to any other server on the MX list. This is to avoid loops. If parrot tries to deliver the mail to itself, a tight loop will ensure. If parrot tries delivering the mail to jay, a big loop ensures because jay would start sending the mail back to parrot, who would send it to jay, and so on. To avoid these loops, a mail server stops delivering the mail when it finds itself in the MX list and queues the mail for later delivery. In effect, a backup server only attempts to deliver mail to MX servers that are more preferred than it. Thus, in this list of three servers, parrot will try to deliver mail only to wren.

Using the same three servers, wren, parrot, and jay, assume that both wren and parrot are down:

+   1. The mail comes to jay.

+   2. jay discovers the more preferred servers are down.

+   3. jay queues the mail for later delivery.

+   4. Later, jay processes its queue. wren is still down but parrot is back in operation.