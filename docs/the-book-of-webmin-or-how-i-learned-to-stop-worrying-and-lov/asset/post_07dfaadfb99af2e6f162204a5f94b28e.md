
## reject_unknown_client

The request will be refused if the client IP has no PTR record in the DNS. This means that a client with an IP address that cannot be resolved to a host name cannot send mail to this host.

## check_client_access maptype:mapname

This option requires the inclusion of an already configured map, as discussed earlier. This will restrict based on the contents of the map, allowing only clients that are allowed by the map. The map may contain networks, parent domains, or client addresses, and Postfix will strip off unnecessary information to match the client to the level of specificity needed.

## check_sender_access maptype:mapname

This will restrict based on the contents of the map, allowing only senders that are allowed by the map. The map may contain networks, parent domains, or localpart@.

## reject_maps_rbl

An RBL is a relay domain black hole list. By testing a reverse domain lookup against a name server that receives a domain black hole list transfer, the server can know if the mail was sent through a known open mail relay. There are a number of free and for-fee services providing black hole data. The largest and longest lasting is the service operated by MAPS [http://www.mail-abuse.org/], while two new similar services are operated by the Open Relay Database [http://ordb.org/] and by Distributed Sender Boycott List [http://dsbl.org/]. All operated on the principle of allowing administrators to choose to refuse mail sent from open mail relays. If this option is listed, the client will be checked against the available RBL domains, and if any match the mail will be refused.

> NOTE If using any of the free RBL services on the network, consider donating money, time, or resources to the project maintainers. The projects are generally run by volunteer labor, using network resources that have been paid for by the maintainers.

## reject_invalid_hostname

If the client host name is invalid, due to bad syntax, the request will be rejected.

## permit_naked_ip_address

If the client HELO or EHLO command contains a naked IP address without the enclosing [] brackets as required by the mail RFC, the message will be rejected. Beware that some popular mail clients send a HELO greeting that is broken this way.

## reject_unknown_hostname

Reject the request if the host name in the client HELO command has no A or MX record in the DNS.

## reject_non_fqdn_hostname

If the client host name is not in the form of a fully qualified domain name, as required by the RFC, the message will be rejected.

```
check_helo_access maptype:mapname
```

The server will search the named access database map for the HELO host name or parent domains. If the result from the database search is REJECT or a 4xx text or 5xx text error code the message will be refused, while a response of OK or RELAY or an all numerical response will permit the message.

```
permit
```

This simply permits anything. Generally this will be at the end of a set of restrictions in order to allow anything that has not been explicitly prohibited.

```
reject
```

Rejects everything. This can be used at the end of a chain of restrictions to prohibit anything that has not been explicitly permitted.

```
warn_if_reject
```

This is a special option that changes the meaning of the following restriction, so that a message that would have been rejected will be logged but still accepted. This can be used for testing new rules on production mail servers without risk of denying mail due to a problem with the rules.

```
reject_unauth_pipelining
```

If the client sends commands ahead of time without first confirming that the server support SMTP command pipelining, the message will be rejected. This will prevent mail from some poorly written bulk email software that improperly uses pipelining to speed up mass deliveries.

## Restrictions on client hostnames/addresses

This restriction applies to the client host name and/or address. By default, Postfix will allow connections from any host, but you may add additional restrictions using the following: reject_unknown_client, permit_mynetworks, check_client_access maptype:mapname, reject_maps_rbl, maps_rbl_reject_code, permit, reject, warn_if_reject, reject_unauth_pipelining.

## Restrictions on sends in HELO commands

This option specifies additional restrictions on what information can be sent by client in the HELO and EHLO commands. This option correlates to the smtpd_helo_restrictions directive. By default Postfix accepts anything, and the following restrictions may be added: reject_invalid_hostname, permit_naked_ip_address, reject_unknown_hostname, reject_non_fqdn_hostname, check_helo_access maptype:mapname, reject_maps_rbl, reject_unknown_client, check_client_access maptype:mapname, permit, reject, warn_if_reject, reject_unauth_pipelining.

## Restrictions on sender addresses

This option restricts what can be contained in the MAIL FROM command in a message. It may be used to prevent specific email addresses from sending mail, reject clients without a resolvable host name, and so on. This option correlates to the smtpd_sender_restrictions directive and may contain any of the following

```
restrictions: permit_mynetworks:, reject_unknown_client, reject_maps_rbl,
reject_invalid_hostname, reject_unknown_hostname, reject_unknown_sender_domain,
check_sender_access maptype:mapname, check_client_access maptype:mapname,
check_helo_access maptype:mapname, reject_non_fqdn_hostname, reject_non_fqdn_sender,
reject, permit.
```

## Restrictions on recipient addresses

This parameter places restrictions on the recipients that can be contained in the RCPT TO command of a sent message. It can be used to dictate where email may be sent. This option correlates to the smtpd_recipient_restrictions and may contain any of the following restrictions: permit_mynetworks, reject_unknown_client, reject_maps_rbl, reject_invalid_hostname, reject_unknown_hostname, reject_unknown_sender_domain, check_relay_domains, permit_auth_destination, reject_unauth_pipelining, permit_mx_backup, reject_unknown_recipient, check_recipient_access, check_client_access, check_helo_access, check_sender_access, reject_non_fqdn_hostname, reject_non_fqdn_sender, reject_non_fqdn_recipient, reject, permit.

## DNS domains for blacklist lookups

This option configures the optional blacklist DNS servers that will be used for all RBL checks that have been specified in all access restrictions. It may contain any number of servers in a whitespace separated list. These services can be used to help prevent spam, as discussed earlier in this section, with the Restrict ETRN command upon parameter. This option configures the maps_rbl_domains directive and is empty by default.

## Restrict mail relaying

This option specifies from which hosts, networks, domains, and so on. Postfix will relay email for. This option correlates to the relay_domains directive and defaults to $mydestination.

## SMTP server response on access map violation, SMTP server response on RBL domains violation, SMTP server response on forbidden relaying, SMTP server response on unknown client reject, SMTP server response on invalid hostname reject, SMTP server response on unknown domain reject, SMTP server response on unknown hostname reject

These options configure the error result code that will be sent to the client when any of the specified restrictions are being applied. These errors have sensible default values and generally should not need to be changed. Consult with RFC 822 if you wish to understand more about the SMTP error codes or have a reason to change any of these values.

## SMTP Client Options

The SMTP client options configures how Postfix will behave when dealing with other mail servers as a client, e.g., when sending mail on behalf of a user. This portion of the configuration primarily dictates how the server will respond to certain error conditions.

## Action when listed as best MX server

As discussed in the BIND chapter, a mail server performs a name server query to find the MX, or mail server, record for the destination domain. If this record indicates that the local server is the server to which mail should be sent, it can respond in a couple of ways. The default is to bounce the message with an error indicating a mail loop. If the field is selected and local is entered, the mail will be directed to the local delivery agent instead of bouncing the mail. This option correlates to the best_mx_transport directive.

## Hosts/domains to hand off mail to on invalid destination

By default, mail that cannot be delivered because the destination is invalid will be bounced with an appropriate error message. However, it is possible to configure postfix to hand off email to another server instead. This option correlates to the fallback_relay directive.

## Ignore MX lookup error

If a name server query fails to provide an MX record, the server defaults to deferring the mail and trying again later. If Yes is selected instead, an A record query will be done and an attempt will be made to deliver to the resulting address. This option correlates to the ignore_mx_lookup_error directive.

## Skip 4xx greeting

If a remote server responds to a connection with a 4XX status code, Postfix will, by default, select the next available mail exchanger specified by the MX records. If set to No, mail delivery will be deferred after the first mail delivery attempt, and another attempt will be made later. This option correlates to the smtp_skip_4xx_greeting directive.

## Skip wait for the QUIT command

This option configures whether Postfix will wait for the receiving mail server to respond to the QUIT command. This option correlates to the smtp_skip_quit_response directive and defaults to no.
