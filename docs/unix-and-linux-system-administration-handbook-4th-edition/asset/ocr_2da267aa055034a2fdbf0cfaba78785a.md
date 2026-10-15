# Table 20.11 Basic sendmail configuration options

|  | Option name | Description (default value) |
|---|---|---|
| Resources | MAX_DAEMON_CHILDREN | Max number of child processes* (no limit) |
|  | MAX_MESSAGE_SIZE | Max size in bytes of a single message (infinite) |
|  | MIN_FREE_BLOCKS | Min filesystem space to accept mail (100) |
|  | TO_lots_of_stuff | Timeouts for all kinds of things (various) |
|  | DELAY_LA | Load avg. to slow down deliveries (0 = no limit) |
|  | FALLBACK_MX | See page 803 for description (no default) |
|  | FAST_SPLIT | Suppresses MX lookups as recipients are sorted and split across queues (1 = true) |
| Performance | HOST_STATUS_DIRECTORY | See page 803 for description (no default) |
|  | MCI_CACHE_SIZE | # of open outgoing TCP connections cached (2) |
|  | MCI_CACHE_TIMEOUT | Time to keep cached connections open (5m) |
|  | MIN_QUEUE_AGE | Minimum time jobs must stay in queue; makes a busy machine handle the queue better (0) |
|  | QUEUE_LA | Load average at which mail should be queued instead of delivered immediately (8 * #CPUs) |
|  | REFUSE_LA | Load avg. at which to refuse mail (12 * #CPUs) |
| Security and spam | AUTH_MECHANISMS | SMTP auth mechanisms for Cyrus SASLᵇ |
|  | CONNECTION_RATE_THROTTLE | Slows DOS attacks by limiting the rate at which mail connections are accepted (no limit) |
|  | DONT_BLAME_SENDMAIL | Overrides sendmail's security and file checking; don't change casually! (safe) |
|  | MAX_MIME_HEADER_LENGTH | Sets max size of MIME headers (no limit)ᶜ |
|  | MAX_RCPTS_PER_MESSAGE | Slows spam delivery; defers extra recipients and sends a temporary error msg (infinite) |
|  | PRIVACY_FLAGS | Limits info given out by SMTP (authwarnings) |
| Misc | DOUBLE_BOUNCE_ADDRESS | Catches a lot of spam; some sites use /dev/null, but that can hide serious problems (postmaster) |
|  | LDAP_DEFAULT_SPEC | Map spec for LDAP database, including the host and port the server is running on (undefined) |

a. More specifically, the maximum number of child processes that can run at once. When the limit is reached, sendmail refuses connections. This option can prevent (or create) denial of service attacks.
b. The default value is EXTERNAL GSSAPI KERBEROS V4 DIGEST-MD5 CRAM-MD5; don't add PLAIN LOGIN, because the password is transmitted as cleartext. That may be OK internally, but not on the Internet unless the connection is also secured through the use of SSL or TLS.
c. This option can prevent user agent buffer overflows. 256/128* is a good value to use—it means 256 bytes per header and 128 bytes per parameter to that header.

Couple these with techniques like greylisting (page 764), content scanning with amavisd-new (page 769), and the new DNS records for email authentication (page 767), and you might stand a fighting chance against the spammers.