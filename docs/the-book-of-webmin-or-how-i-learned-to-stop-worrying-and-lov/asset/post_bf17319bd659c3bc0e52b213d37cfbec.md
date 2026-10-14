
## Max number of parallel deliveries to the same destination

This option specifies the maximum number of deliveries that Postfix will perform to the same destination simultaneously. This option correlates to the smtp_destination_concurrency_limit directive and defaults to the system-wide limit for parallel deliveries configured in the Delivery Rates page documented in the next section.

## Max number of recipients per delivery

Limits the number of recipients per delivery. This option correlates to the smtp_destination_recipient_limit directive and defaults to the system-wide limit for recipients per delivery.

## Timeout for completing TCP connections

Specifies the time in seconds that the Postfix delivery agent will wait before timing out a TCP connection. This option correlates to the smtp_connect_timeout directive and defaults to 0, which disables connection timeouts.

## Timeout on waiting for the greeting banner

Limits how long Postfix will wait for a greeting banner to be received from the destination server. This option corresponds to the smtp_helo_timeout directive and defaults to 300 seconds.

## Timeout on waiting for answer to MAIL FROM

Sets the timeout in seconds for sending the SMTP MAIL FROM command and for receiving the destination server's response. This option correlates to the smtp_mail_timeout directive and defaults to 300 seconds.

## Timeout on waiting for answer to RCPT TO

Sets the timeout in seconds for sending the SMTP RCPT TO command and for receiving the destination server's response. This option correlates to the smtp_rcpt_timeout directive and defaults to 300 seconds.

## Timeout on waiting for answer to DATA

Sets the timeout in seconds sending the SMTP DATA command and for receiving the destination server's response. This option correlates to the smtp_data_init_timeout directive and defaults to 120 seconds.

## Timeout on waiting for answer to transmit of message content

Specifies the SMTP client timeout in seconds for sending the contents of the message. If the connection stalls for longer than this timeout, the delivery agent will terminate to transfer. This option corresponds to the smtp_data_xfer_timeout directive and defaults to 180 seconds.

## Timeout on waiting for answer to ending "."

Specifies the SMTP client timeout in seconds for sending the closing SMTP "." and receiving the destination server's reply. This option correlates to the smtp_data_done_timeout directive and defaults to 600 seconds.

## Timeout on waiting for answer to QUIT

Sets the timeout in seconds sending the SMTP QUIT command and for receiving the destination server's response. This option correlates to the smtp_quit_timeout directive and defaults to 300 seconds.

## Delivery Rates

This page contains the options for setting the default rate and concurrency limits for all Postfix components. These rates can usually be overridden within their respective configuration sections.

## Max number of parallel deliveries to the same destination

This option specifies the maximum number of deliveries that Postfix will perform to the same destination simultaneously. This option correlates to the default_destination_concurrency_limit directive and defaults to 10.

## Max number of recipients per message delivery

Limits the number of recipients per delivery. This option correlates to the default_destination_recipient_limit directive and defaults to 50.

## Initial concurrency level for delivery to the same destination

Specifies the initial number of simultaneous deliveries to the same destination. This limit applies to all SMTP, local, and pipe mailer deliveries. A concurrency of less than two could lead to a single problem email backing up delivery of other mail to the same destination. This option configures the initial_destination_concurrency directive and defaults to 5.

## Max time (days) in queue before message is undeliverable

Defines the number of days a message will remain queued for delivery in the event of delivery problems before the message is sent back to the sender as undeliverable. This option configures the maximal_queue_lifetime directive and defaults to 5 days.

## Min time (secs) between attempts to deliver a deferred message

In the event of a delivery deferral, Postfix will wait the specified amount of time before reattempting delivery. This value also specifies the time an unreachable destination will remain in the destination status cache. This option correlates to the minimal_backoff_time directive and defaults to 1000 seconds.

## Max time (secs) between attempts to deliver a deferred message

Specifies the maximum amount of time between delivery attempts in the event of a deferred delivery. This option configures the maximal_backoff_time directive and defaults to 4000 seconds.

## Time (secs) between scanning the deferred queue

Specifies the time in seconds between queue scans by the queue management task. This option correlates to the queue_run_delay and defaults to 1000 seconds.

## Transports that should not be delivered

This field specifies which delivery transports, if any, of the transports defined in the Transport Mapping section will not have their messages sent automatically. Instead the messages for these transports will be queued and can be delivered manually using the sendmail -q command. This option correlates to the defer_transports directive and contains nothing by default.

## Debugging Features

Postfix has two levels of logging. The first level is the normal maillog, which reports on all normal mail activities such as received and sent mail, server errors, shutdowns, and startups. The second level is more verbose and can be tuned to log activity relating to specific SMTP clients, host names, or addresses. This page contains the configuration for the second level of logging.

## List of domain/network patterns for which verbose log is enabled

This is a list of patterns or addresses that match the clients, hosts, or addresses whose activity you would like to have more verbose logging for. Values here could be an IP address like 192.168.1.1 or a domain name like swelittec.com. This option correlates to the debug_peer_list directive and is empty by default.

## Verbose logging level when matching the above list

Specifies the level of verbosity of the logging for the activity that matches the above patterns. This option correlates to the debug_peer_level directive and defaults to 2. The above field must have at least one value for this debug level to have any impact.

## Postfix, Unsolicited Commercial Email, and Access Controls

Postfix offers an extremely flexible set of access controls, primarily targeted at preventing unsolicited commercial email from being delivered through the server. In order to construct a suitable set of controls it is necessary to understand the order in which rules are checked and how they interact. By default Postfix will accept mail for delivery from or to any client on your local network and any
domains that are hosted by Postfix. So, by default, Postfix is not an open relay. This is a good beginning and may be all that is needed in many environments. However, because UCE is such a nuisance for users and network administrators, it may be worthwhile to implement more advanced filtering. This section will address the basics of the Postfix UCE control features.

## Access Control List Order

Every message that enters the smtpd delivery daemon will be processed by a number of access control lists and checked against a number of rules to ensure that the message is one that the administrator actually wants delivered. The goal for most administrators is to prevent unsolicited commercial email from passing through these rules, yet allow every legitimate email to be delivered. This is a lofty goal and a delicate balance. No perfect solution exists, as long as people are willing to steal the resources of others for their own commercial gain and go to great lengths to overcome the protections in place to prevent such abuse. However, in most environments it is possible to develop a reasonable set of rules that prevents most spam and allows most or all legitimate mail through unharmed.

It is important to understand the order of processing if complex sets or rules are to be used, as attempting to use a particular rule too early in the chain can lead to subtle errors or strange mail client behavior. Because not all clients react exactly correctly to some types of refusals, and not all clients create correctly formed SMTP requests, it is not unlikely that a misplaced rule will lock out some or all of your clients from sending legitimate mail. It could also just as easily lead to opening a hole in your spam protections early in the rule set, which would allow illicit mail to pass.

The Postfix UCE controls begin with a couple of simple yes or no checks, called smtpd_helo_required and strict_rfc821_envelopes, both configured in the SMTP Server Options page. The first, if enabled, requires a connecting mail client to introduce itself fully by sending a HELO command. This can stop some poorly designed bulk email programs. The second option requires for the envelope to fit the SMTP specification precisely, thus enforcing complete headers. Though the envelope and HELO can be forged by a bulk mailer, it may stop the more hastily implemented variants (well, how many good programmers do you know that write tools to help spammers?).

The next stage is the four SMTP restrictions also found on the SMTP Server Options page. These further limit from where and to where mail will be delivered. The order of traversal for these four lists of rules is:

- 1. **Restrictions on client hostnames/addresses** or `smtpd_client_restrictions`
- 2. **Restrictions on sends in HELO commands** or `smtpd_helo_restrictions`
- 3. **Restrictions on sender addresses** or `smtpd_sender_restrictions`
- 4. **Restrictions on recipient addresses** or `smtpd_recipient_restrictions`

Each of these checks can return REJECT, OK, or DUNNO. If REJECT, the message will be refused, and no further rules will be checked. If OK, no further rules in the given restriction will be checked, and the next restriction list will be checked. If
