# 20.11 Basic sendmail configuration options

| Option name | Description (default value)ᵃ |
| --- | --- |
| Resources | MAX_DAEMON_CHILDREN | Max number of child processes (no limit)\nMAX_MESSAGE_SIZE | Max size in bytes of a single message (infinite)\nMAX_FREE_BLOCKS | Min filesystem space to accept mail (100)\nTO_lots_of_stuff | Timeouts for all kinds of things (variable)|
| Performance | DELAY_LA | Load avg. to slow deliveries (0 = no limit)\nFALLBACK_MX | See page 803 for description (no default)\nFAST_SPLIT | Suppresses MX lookups as recipients are sorted and split across queues (1 = true)\nHOST_STATUS_DIRECTORY | See page 803 for description (no default)\nMCI_CACHE_SIZE | # of opening TCP connections cached (2)\nMCI_CACHE_TIMEOUT | Time to keep cached connections\nMIN_QUEUE_AGE | Minimum time must stay in queue; makes a busy machine to handle the queue buffer (0)\nQUEUE_LA | Load average at which mail should be queued instead of delivered immediately (8 * IPCUs)\nREFUSE_LA | Load avg. to refuse mail (12 * IPCUs)|
| Security and spam | AUTH_MECHANISMS | SMTP auth mechanisms for Cyrus SASLB\nCONNECTION_RATE_THROTTLE | Slows DDoS attacks by limiting the rate at which mail connections are accepted (no limit)\n_SENDMAIL | Overrides sendmail's security and file checking; don't change usually! (safe)\nMAX_MIME_HEADER_LENGTH | Sets size of MIME headers (no limit)\nMAX_RCPTS_PER_MESSAGE | Slows spam delivery; defers extra recipients and sends a temporary error message (info)\nPRIVACY_FLAGS | Limits info out by SMTP (authwarnings)|
| Misc | DOUBLE_BOUNCE_ADDRESS | Catches a lot of spam; some use use/null, but that can cause serious problems (postmaster)\nLDAP_DEFAULT_SPEC | Map spec for LDAP database, including the host and the port is running (undefined)|

> a. Specifically, the maximum number of child processes that can run at once. When the limit is reached, sendmail refuses connections. This option can prevent (or) denial of service attacks.
b. The default value is EXTERNAL GSAPI KERBEROS_V4 DIGEST-MD5 CRM-MD5; don't add LOGIN, because the password is transmitted as cleartext. That may be OK internally, but not unless the Internet connection is also secured through the use of SSL.
c. This option can prevent user agent buffer. "256/128" is a good value to use—it means 256 bytes per header and 128 bytes per parameter to header.

Couple these with techniques like greylisting (page 764), content scanning with amavisird-new (page 769), and the new DNS records for email authentication de (page 767), and you might stand a fighting chance against the spammers.