# Local scan function

my_remote_delivery:
driver = smtp

my_remote_delivery_port587:
driver = smtp
port = 587
headers_add = X-processed-by: MACRO_HEADER port

The second instance, my_remote_delivery_port587, specifies the port and also a header to be added to the message that includes an indication of outgoing port. MACRO_HEADER would be defined elsewhere in the configuration file.

# Retry configuration

The retry section of the configuration file must exist or Exim will never attempt redelivery of messages that could not be delivered on the first attempt. You can specify three intervals, each less frequent than the previous one. After the last interval has expired, messages bounce back to the sender as undeliverable. retry understand the suffixes m, h, d, and w to indicate minutes, hours, days, and weeks. You can specify different intervals for different hosts or domains.

Here's what a retry section looks like:

```
begin retry
* F, 2h, 15m; F, 24h, 1h; F, 4d, 6h
```

This example means, "For any domain, an address that fails temporarily should be retried 15 minutes for 2 hours, then every hour for the next 24 hours, then every 6 hours for 4 days, and finally, bounced as undeliverable."

# Rewriting configuration

The rewriting section of the configuration file starts with begin rewrite. It's used to fix addresses, not to reroute messages. For example, you could use it on your outgoing addresses

+   * To make mail appear to be from your domain, not from individual hosts
* To map usernames to a standard format as First.Last

Rewriting should not be used on addresses in incoming mail.

# Local scan function

If you want to further customize exim, for example, to filter for the latest and greatest virus, you can write a C function to do your scanning and install it in the local_scan section of the config file. Refer to the Exim documentation for examples that show how to do this.