# Max time (secs) between attempts to deliver a deferred message

Specifies the maximum amount of time between delivery attempts in the event of a deferred delivery. This option configures the maximal_backoff_time directive and defaults to 4000 seconds.

# Time (secs) between scanning the deferred queue

Specifies the time in seconds between queue scans by the queue management task. This option correlates to the queue_run_delay and defaults to 1000 seconds.

# Transports that should not be delivered

This field specifies which delivery transports, if any, of the transports defined in the Transport Mapping section will not have their messages sent automatically. Instead the messages for these transports will be queued and can be delivered manually using the sendmail -q command. This option correlates to the defer_transports directive and contains nothing by default.

# Debugging Features

Postfix has two levels of logging. The first level is the normal maillog, which reports on all normal mail activities such as received and sent mail, server errors, shutdowns, and startups. The second level is more verbose and can be tuned to log activity relating to specific SMTP clients, host names, or addresses. This page contains the configuration for the second level of logging.

# List of domain/network patterns for which verbose log is enabled

This is a list of patterns or addresses that match the clients, hosts, or addresses whose activity you would like to have more verbose logging for. Values here could be an IP address like 192.168.1.1 or a domain name like swelittec.com. This option correlates to the debug_peer_list directive and is empty by default.

# Verbose logging level when matching the above list

Specifies the level of verbosity of the logging for the activity that matches the above patterns. This option correlates to the debug_peer_level directive and defaults to 2. The above field must have at least one value for this debug level to have any impact.

# Postfix, Unsolicited Commercial Email, and Access Controls

Postfix offers an extremely flexible set of access controls, primarily targeted at preventing unsolicited commercial email from being delivered through the server. In order to construct a suitable set of controls it is necessary to understand the order in which rules are checked and how they interact. By default Postfix will accept mail for delivery from or to any client on your local network and any