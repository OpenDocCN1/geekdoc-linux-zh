+   The MAX_RUNNERS_PER_QUEUE option sets the default runner limit per queue if no explicit value is set with the Runners= (or R=) parameter in the queue group definition.

# Load average controls

sendmail has always been able to refuse connections or queue messages instead of delivering them when the system load average goes too high. Unfortunately, the load average has only a one-minute granularity, so it’s not a very finely honed tool for smoothing out the resources consumed by sendmail. The DELAY_LA primitive lets you set a value of the load average at which sendmail should slow down; it will sleep for one second between SMTP commands for current connections and before accepting new connections. The default value is 0, which turns the mechanism off.

# Undeliverable messages in the queue

Undeliverable messages in the mail queue can really kill performance on a busy mail server. sendmail has several features that help with the issue of undeliverable messages. The most effective is the FALLBACK_MX option, which hands a message off to another machine if it cannot be delivered on the first attempt. Your primary machine cranks out the messages to good addresses and shunts the problem children to a secondary fallback machine. Another aid is the host status directory, which stores the status of remote hosts across queue runs.

The FALLBACK_MX option is a big performance win for a site with large mailing lists that invariably contain addresses that are temporarily or permanently undeliverable. To use it, you specify the host to handle the deferred mail. For example,

```
define(`confFALLBACK_MX', `mailbackup.atrust.com')
```

forwards messages that fail their first delivery attempt to mailbackup.atrust.com for further processing. There can be multiple fallback machines if the designated hosts have multiple MX records in DNS.

The TO_ICONNECT option sets a timeout on the initial attempt to connect and send a message. If you set it short, more work is shunted to the fallback MTA. However, it does let the main server whip through the first pass at a large mailing list in record time.

On the fallback machines, you can use the HOST_STATUS_DIRECTORY option to help with multiple failures. This option directs sendmail to maintain a status file for each host to which mail is sent and to use that status information to prioritize the hosts each time the queue is run. This status information effectively implements negative caching and allows information to be shared across queue runs. It’s a performance win on servers that handle mailing lists with a lot of bad addresses, but it can be expensive in terms of file I/O.