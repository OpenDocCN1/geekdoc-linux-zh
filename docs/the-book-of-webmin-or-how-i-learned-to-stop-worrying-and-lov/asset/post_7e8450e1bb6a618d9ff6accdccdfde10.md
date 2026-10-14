
> NOTE If adding aliases from the command line, it is possible to regenerate the aliases database using the command postalias. The man page for this command is a useful resource for understanding how aliases databases are handled in Postfix.

## Canonical Mapping

Canonical mapping in Postfix is used for modifying mail in the incoming queue, and it alters both the message headers and the message envelope information for local or remote mail. This mapping can be useful to replace login names with Firstname.Lastname style addresses, or to clean up odd addresses produced by legacy mail systems.

## Canonical Mapping Tables

If you use any canonical mapping tables, they must be specified in the first section of the Canonical Mapping module. After defining them, you can edit them from the second section of the module.

## Address mapping lookup tables

This option specifies the location of the optional canonical address mapping table file. This mapping is applied to both sender and recipient addresses, in both envelopes and headers. This option configures the canonical_maps directive and is disabled by default. Much like the aliases files discussed in the last section, canonical mapping files are specified by a database type and a filename. The accepted database types depend on your operating system, and installed components. Usually hash and dbm are used as the database type. A common choice for this value, then, might be hash:/etc/postfix/canonical.

## Tables for RECIPIENT addresses

This parameter configures address mapping only on recipient addresses, and not sender addresses. Mapping is performed on both envelopes and headers. These lookups are performed before the above configured Address mapping lookup tables. This option correlates to the recipient_canonical_maps directive and is disabled by default.

## Tables for SENDER addresses

Similar to the previous option, this configures mapping for sender addresses only, and not recipient addresses. Both envelope and header information is modified. This option correlates to the sender_canonical_maps directive and by default is disabled.

## Editing Canonical Mappings

Once a filename is selected for any of the canonical mapping tables, it may be edited by clicking the appropriate Edit buttons. A new page will open, listing any existing mappings and allowing creation of new mappings. The format of mappings in all files is the same.

Canonical mappings may seem, on the surface, to be similar to aliases or virtual domains. However, they are quite distinct and are useful for other purposes. While aliases merely make a decision about which user will receive an email, and virtual domains only impact the envelope address, the canonical mapping alters both the envelope address and the SMTP header address. This change can be used to make mail appear to come from a different user or domain, or direct mail to a different user or domain by changing the address on the message.

For example, if I have a number of local subdomains, but would like all mail to appear to originate from a single domain, it is possible to create a canonical mapping to make the translations. In the Edit a Map page, the Name will be a subdomain that is to be mapped to the domain, such as @lab.swellitech.com. The Maps to... value will simply be the domain I'd like this subdomain converted to, @swellitech.com. After saving the mapping and applying changes, all outgoing mail from lab.swellitech.com will appear to originate from swellitech.com.

## Virtual Domains

Virtual domains functionality in Postfix provides a means to redirect messages to different locations by altering the message envelope address. The header address is not altered by a virtual domain mapping. While some functionality of virtual domains overlaps with features available in aliases, virtual domains can be used for local or non-local addresses, while aliases can only be used for local address.

## Domain mapping lookup tables

Much like aliases tables and canonical mapping tables discussed in the previous sections, this is simply the path to a file containing the mapping tables for virtual domains. This is usually something along the lines of hash:/etc/postfix/virtual, and must be converted to a database format for use in Postfix. Webmin will perform the database generation step for you.

## Transport Mapping

The term transport refers to the mechanism used to deliver a piece of email. Specifically, SMTP and UUCP are mail transports that are supported by Postfix. Transport mapping can be used for a number of purposes, including SMTP to UUCP gatewaying, operating Postfix on a firewall with forwarding to an internal mail server, and so on.

## Transport mapping lookup tables

This option configures the path to a file containing one or more transport mappings. These tables are much like the mapping tables discussed already, and are converted to a database and used by Postfix in the same way. This option correlates to the transport_maps directive. This feature is disabled by default. A common value for this option is /etc/postfix/transport.

To create a new mapping, first define the mapping file. Then click Add a mapping. If your goal is to redirect mail to an protected internal host from Postfix running on a firewall, for example, you could enter the outside domain name into the Name field, swelltech.com and then enter into the Maps to field the address of the internal machine, smtp:privatehost.swelltech.com. To further improve upon this, local delivery on this machine could be disabled, and increased controls over where and to whom mail should be accepted. There are more examples of such a configuration in the tutorial section of this chapter.

## Relocated Mapping

Using this option it is possible to notify senders if a local user has moved to another address. For example, if a user leaves an organization but still receives occasional mail at her local address, it may be convenient to notify anyone sending mail to the user of the move and new contact information for that user. Usage is just like the previous types of mappings and so won’t be documented specifically here, though an example of a relocated mapping will be given to display the types of information that can be provided by this feature.

As an example, let’s say I move from my current company to the far more relaxed atmosphere of the Oval Office. To make sure all of my friends and clients can keep in touch with me, I could provide a relocated mapping with a Name of joe@swelltech.com with a Maps to of president@whitehouse.gov. While this won’t redirect mail to me at my new home, it will notify the people trying to contact me that I’ve changed email addresses. Hopefully they will all update their address books and resend their mail to my new address.

## Local delivery

Local delivery is what Postfix does when it reaches the end of all of its list of mappings and access controls, and still finds that the message is allowed and destined for a user on the local machine (i.e., a mapping could potentially send the message elsewhere for final delivery, so all mappings as well as various access checks are performed before reaching this stage). This page configures a number of options relating to how Postfix handles the delivery of mail for local users (Figure 10-5).

![](img/d84604054810a13cacfdac212ebee2f7_201_0.png)

Figure 10-5: Local Delivery

## Name of the transport for local deliveries

This configures the name of the transport that will be used for delivery to destination that match the $mydestination or $inet_interfaces variables. This can be a simple mailbox drop handled by the Postfix local delivery agent, or any appropriate delivery command. This option correlates to the local_transport directive and defaults to the defined transport type named local.

## Shell to use for delivery to external command

If a command shell is required to communicate properly with your chosen local delivery transport, this option selects the shell that will be used. By default no shell is used, and the transport command will be executed directly. However, if the command contains shell meta-characters or shell built-in commands they will be passed to /bin/sh or whatever shell you configure here. A popular choice for this is smsh, or Sendmail's Restricted Shell, which is included in recent Sendmail distributions. smsh allows for more precise control over what commands users can execute from their .forward files. This option corresponds to the local_command_shell and defaults to /bin/sh.

## Search list for forward

This is a comma-separated list of possible locations for user forward files. Postfix will try each entry in the list until a forward file is found or until all have been checked and no match is found. The forward file allows users to configure delivery options for themselves, including delivery-time processing by a program like procmail, as well as forwarding of messages to a different server. A number of variable expansions are performed on the entries. The expansions are currently:
