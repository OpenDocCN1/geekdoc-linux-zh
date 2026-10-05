confTO_RESOLVER_RETRANS Defines, in seconds, the retransmission timer for all resolver lookups. [Timeout.resolver.retrans]

confTO_RESOLVER_RETRANS_FIRST Defines, in seconds, the retransmission timer for the resolver lookup for the first attempt to deliver a message. [Timeout.resolver.retrans.first]

confTO_RESOLVER_RETRANS_NORMAL Defines, in seconds, the retransmission timer for all resolver lookups after the first attempt to deliver a message. [Timeout.resolver.retrans.normal]

confTO_RESOLVER_RETRY Defines the total number of times to retry a resolver query. [Timeout.resolver.retry]

confTO_RESOLVER_RETRY_FIRST Defines the number of times the resolver query for the first attempt is retried. [Timeout.resolver.retry.first]

confTO_RESOLVER_RETRY_NORMAL Defines the number of times to retry resolver queries after the first delivery attempt. [Timeout.resolver.retry.normal]

confTO_RSET Sets the maximum time to wait for a RSET command response. Defaults to 5m. [Timeout.rset]

confTRUSTED_USER Defines the users who control the Sendmail daemon and the files created by Sendmail. Do not confuse this option with confTRUSTED_USERS. [TrustedUser]

confTRUSTED_USERS Adds to the list of who can send mail under usernames. This always includes root, ucpd, and daemon. [$==]

confRY_NULL_MX_LIST Tells Sendmail to connect to the remote host directly if the MX record points to the local host. The default is false. [TryNullMXList]

confSAFE_GROUP_WRITES :include and . forward files. Defaults to false. [UnsafeGroupWrites]

confUSERDB_SPEC Defines the path of the user database file. [UserDatabaseSpec]

confERRORS_TO True tells Sendmail to deliver errors using the Errors-To header. Defaults to false. [UserErrorsTo]

confUUCP_MAILER Defines the default mailer. Defaults to uocpd-old.

confWORK_CLASS_FACTOR Defines the factor used to favor high-priority jobs. Defaults to 1800. [ClassFactor]

confWORK_RECIPIENT_FACTOR Defines the factor used to lower the priority of a job for each additional recipient. Defaults to 30000. [RecipientFactor]

confWORK_TIME_FACTOR Defines the factor used to lower the priority of a job for each delivery attempt. Defaults to 90000. [RetryFactor]