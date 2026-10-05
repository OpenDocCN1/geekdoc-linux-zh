
# 20.11 Basic sendmail configuration options

| Option name | Description (default value)ᵃ |
| --- | --- |
| Resources | MAX_DAEMON_CHILDREN | Max number of child processes (no limit)<br>MAX_MESSAGE_SIZE | Max size in bytes of a single message (infinite)<br>MAX_FREE_BLOCKS | Min filesystem space to accept mail (100)<br>TO_lots_of_stuff | Timeouts for all kinds of things (variable) |
| Performance | DELAY_LA | Load avg. to slow deliveries (0 = no limit)<br>FALLBACK_MX | See page 803 for description (no default)<br>FAST_SPLIT | Suppresses MX lookups as recipients are sorted and split across queues (1 = true)<br>HOST_STATUS_DIRECTORY | See page 803 for description (no default)<br>MCI_CACHE_SIZE | # of opening TCP connections cached (2)<br>MCI_CACHE_TIMEOUT | Time to keep cached connections<br>MIN_QUEUE_AGE | Minimum time must stay in queue; makes a busy machine to handle the queue buffer (0)<br>QUEUE_LA | Load average at which mail should be queued instead of delivered immediately (8 * IPCUs)<br>REFUSE_LA | Load avg. to refuse mail (12 * IPCUs) |
| Security and spam | AUTH_MECHANISMS | SMTP auth mechanisms for Cyrus SASLB<br>CONNECTION_RATE_THROTTLE | Slows DDoS attacks by limiting the rate at which mail connections are accepted (no limit)<br>_SENDMAIL | Overrides sendmail's security and file checking; don't change usually! (safe)<br>MAX_MIME_HEADER_LENGTH | Sets size of MIME headers (no limit)<br>MAX_RCPTS_PER_MESSAGE | Slows spam delivery; defers extra recipients and sends a temporary error message (info)<br>PRIVACY_FLAGS | Limits info out by SMTP (authwarnings) |
| Misc | DOUBLE_BOUNCE_ADDRESS | Catches a lot of spam; some use use/null, but that can cause serious problems (postmaster)<br>LDAP_DEFAULT_SPEC | Map spec for LDAP database, including the host and the port is running (undefined) |

a. Specifically, the maximum number of child processes that can run at once. When the limit is reached, sendmail refuses connections. This option can prevent (or) denial of service attacks.
b. The default value is EXTERNAL GSAPI KERBEROS_V4 DIGEST-MD5 CRM-MD5; don't add LOGIN, because the password is transmitted as cleartext. That may be OK internally, but not unless the Internet connection is also secured through the use of SSL.
c. This option can prevent user agent buffer. "256/128" is a good value to use—it means 256 bytes per header and 128 bytes per parameter to header.

Couple these with techniques like greylisting (page 764), content scanning with amavisird-new (page 769), and the new DNS records for email authentication de (page 767), and you might stand a fighting chance against the spammers.

# Relay control

sendmail accepts incoming mail, looks at the envelope addresses, decides where the mail should go, and then passes it along to an appropriate destination. That destination can be local or it can be another transport agent further along in the delivery chain. When an incoming message has no local recipients, the transport agent that handles it is acting as a relay.

Only hosts that are tagged with RELAY in the access database (see page 785) that are listed in /etc/mail/relay-domains are allowed to submit mail for relaying. Some types of relaying are useful and legitimate. How can you tell which messages to relay and which to reject? Relaying is actually necessary in only three situations:

- When the transport agent acts as a gateway for hosts that are not reachable in any other way; for example
- When the transport agent is the outgoing mail server for not-so-smart hosts. In this case, the senders' hostnames or IP addresses will be local (or at least enumerable)
- When you have agreed to be a backup MX destination for another site.

Any other situation that appears to require relaying is probably an indication of bad design (with the possible exception of support for mobile users). You can obfuscate the first use of relaying (above) by designating a centralized server to receive mail, with POP or IMAP being used for client access. The second case should be allowed, but only for your own hosts. You can check IP addresses-or hostnames. In the third case, you can list the other site in your access database and allow relaying just for that site's IP address blocks.

Although sendmail comes with relay turned off, several features have been added to turn relay back on, either in a limited and controlled way. These features are listed below for completeness, but our recommendation is that you be careful about opening things too much. The access_db feature is the safest way to allow relaying.

- FEATURE('relay_entire_domain') – allows relaying for your domain
- RELAY_DOMAIN(domain, ...) – adds more domains to be relayed
- RELAY_DOMAIN_FILE(filename) – same; takes domain list from a file
- FEATURE('relay_hosts_only') – affects RELAY_DOMAIN, accessdb

You will need to make an exception if you use the SMART_HOST or MAIL_HUB designations to route mail through a particular mail server machine. That server will have to be set up to relay mail from local hosts. Configure it with

```
FEATURE('relay_entire_domain')
```

![](img/579efec8c67772f31ecf34844bbb71a2_839_0.png)

# Chapter 20 Electronic Mail

If you consider turning on relaying in some form, consult the sendmail documentation in cf/README to be sure you didn't inadvertently become a friend of spammers. When you are done, have one of the relay-checking sites verify that you did not inadvertently create an open relay—try spamhelp.org.

# User or site blacklisting

If you have local users or hosts to whom you want to block mail, use FEATURE('blacklist_recipients') which supports the following types of entries in your access file:

```
To:nobody@ ERROR:550 Mailbox disabled for this user
To:printer.mydomain ERROR:550 This host does not accept mail
To:user@host.mydomain ERROR:550 Mailbox disabled for this user
```

These lines block incoming mail to user nobody on any host, host printer, to a particular user's address on one machine. The use of DNS: tag lets those users send messages.

# Throttles, rates, and connection limits

| Primitive | Description |
| --- | --- |
| BAD_RCPT_THROTTLE | Slows down incoming connections |
| MAX_RCPTS_PER_MESSAGE | Defers delivery if a message has too many |
| conncontrol | Limits the number of simultaneous connections |
| greet_pause | Delays HELO response, requires strict compliance |

# Throttles, rates, and connection limits

After the login count reaches the limit, use

```
define(confBAD_RCPT_THROTTLE, `3`)
```

Setting the MAX_RCPTS_PER_MESSAGE option causes the sender to queue extra. The ratecontrol and conncontrol features allow per-host or per-net limits on the rate at which incoming connections are accepted and the number of simultaneous connections. Both use the /etc/mail/access file to specify limits that they should obey, the first with tag ClientRate: in the key field and the second with tag Conn:. To enable controls, insert lines like these in .mc file:

```
FEATURE(rate', 'nodelay', terminate)
FEATURE('conncontrol', 'nodelay', terminate)'
```

Then, add to /etc/mail/access the list of hosts or nets to be controlled and their restriction thresholds. For example, the lines

```
ClientRate:172.168.6.17 2
ClientRate:170.65.3.4 10
```

limit the hosts 192.168.6.17 and 170.65.3.4 to two new connections per minute, respectively, the lines

```
ClientConn:192.168.2.8 2
ClientConn:175.14.4.1 7
ClientConn: 10
```

set limits of two simultaneous connections for 192.168.2.8, for 175.14.4.1, and ten simultaneous connections for all hosts.

Another nifty feature is greet_pause. When a remote MTA connects to your sendmail server, the SMTP protocol mandates that it wait for your server's coming greeting before speaking. However, it's common for spam mailers to blunt an EHLO command immediately during the planned awkward moment. Whatever the cause, this behavior is suspicious and is known as 'slamming'.

The greet_pause feature makes sendmail wait for a specified period of time at the beginning of the connection greeting its newfound friend. The remote MTA does not wait to be properly greeted and proceeds with an EHLO or HELLO command during the planned awkward moment, sendmail logs an error and refuses subsequent commands from the remote MTA.

+   12. FEATURE(access_db) must be there too.
