Canonical mappings may seem, on the surface, to be similar to aliases or virtual domains. However, they are quite distinct and are useful for other purposes. While aliases merely make a decision about which user will receive an email, and virtual domains only impact the envelope address, the canonical mapping alters both the envelope address and the SMTP header address. This change can be used to make mail appear to come from a different user or domain, or direct mail to a different user or domain by changing the address on the message.

For example, if I have a number of local subdomains, but would like all mail to appear to originate from a single domain, it is possible to create a canonical mapping to make the translations. In the Edit a Map page, the Name will be a subdomain that is to be mapped to the domain, such as @lab.swellitech.com. The Maps to... value will simply be the domain I'd like this subdomain converted to, @swellitech.com. After saving the mapping and applying changes, all outgoing mail from lab.swellitech.com will appear to originate from swellitech.com.

# Virtual Domains

Virtual domains functionality in Postfix provides a means to redirect messages to different locations by altering the message envelope address. The header address is not altered by a virtual domain mapping. While some functionality of virtual domains overlaps with features available in aliases, virtual domains can be used for local or non-local addresses, while aliases can only be used for local address.

# Domain mapping lookup tables

Much like aliases tables and canonical mapping tables discussed in the previous sections, this is simply the path to a file containing the mapping tables for virtual domains. This is usually something along the lines of hash:/etc/postfix/virtual, and must be converted to a database format for use in Postfix. Webmin will perform the database generation step for you.

# Transport Mapping

The term transport refers to the mechanism used to deliver a piece of email. Specifically, SMTP and UUCP are mail transports that are supported by Postfix. Transport mapping can be used for a number of purposes, including SMTP to UUCP gatewaying, operating Postfix on a firewall with forwarding to an internal mail server, and so on.

# Transport mapping lookup tables

This option configures the path to a file containing one or more transport mappings. These tables are much like the mapping tables discussed already, and are converted to a database and used by Postfix in the same way. This option correlates to the transport_maps directive. This feature is disabled by default. A common value for this option is /etc/postfix/transport.