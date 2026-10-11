If the name of a domain is provided, Postfix determines the relay host for the domain by an MX lookup.

If Postfix should forward all emails that cannot be locally delivered to a relay host without carrying out an MX lookup, the host name of the relay must be given in square brackets (for example, **\[mailrelay.digitalairlines.com\]**).

It is also possible to give an IP address in this form. Optionally, the domain or host can be extended with a port number (for example, **digitalairlines.com:1025**).

If you leave this entry empty, Postfix delivers all mails that cannot be delivered locally to the mail exchanger.

Any entries in the file `/etc/postfix/transport` have precedence over the relay host.

If this variable is assigned a value, the variable `relayhost` in the file `/etc/postfix/main.cf` will be modified by running **SuSEconfig**.

+   * **POSTFIX_MASQUERADE_DOMAIN.** If your own DNS domain is configured with this variable (for example, digitalairlines.com), all addresses in emails that contain a host prefix are shortened by this host prefix.
+     
+     For example, geeko@da2.digitalairlines.com becomes geeko@digitalairlines.com.
+     
+     If this variable is assigned a value, the variable `masquerade_domains` in the file `/etc/postfix/main.cf` is modified by running **SuSEconfig**. Additionally, the variable `masquerade_exceptions` = root will be set.

+   * **POSTFIX_LOCALDOMAINS.** Contains a comma-separated list of the domains for which Postfix should accept emails.
+     
+     These values are written to the variable `mydestination` in the file `/etc/postfix/main.cf` by running **SuSEconfig**.