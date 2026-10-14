> NOTE If adding aliases from the command line, it is possible to regenerate the aliases database using the command postalias. The man page for this command is a useful resource for understanding how aliases databases are handled in Postfix.

# Canonical Mapping

Canonical mapping in Postfix is used for modifying mail in the incoming queue, and it alters both the message headers and the message envelope information for local or remote mail. This mapping can be useful to replace login names with Firstname.Lastname style addresses, or to clean up odd addresses produced by legacy mail systems.

# Canonical Mapping Tables

If you use any canonical mapping tables, they must be specified in the first section of the Canonical Mapping module. After defining them, you can edit them from the second section of the module.

# Address mapping lookup tables

This option specifies the location of the optional canonical address mapping table file. This mapping is applied to both sender and recipient addresses, in both envelopes and headers. This option configures the canonical_maps directive and is disabled by default. Much like the aliases files discussed in the last section, canonical mapping files are specified by a database type and a filename. The accepted database types depend on your operating system, and installed components. Usually hash and dbm are used as the database type. A common choice for this value, then, might be hash:/etc/postfix/canonical.

# Tables for RECIPIENT addresses

This parameter configures address mapping only on recipient addresses, and not sender addresses. Mapping is performed on both envelopes and headers. These lookups are performed before the above configured Address mapping lookup tables. This option correlates to the recipient_canonical_maps directive and is disabled by default.

# Tables for SENDER addresses

Similar to the previous option, this configures mapping for sender addresses only, and not recipient addresses. Both envelope and header information is modified. This option correlates to the sender_canonical_maps directive and by default is disabled.

# Editing Canonical Mappings

Once a filename is selected for any of the canonical mapping tables, it may be edited by clicking the appropriate Edit buttons. A new page will open, listing any existing mappings and allowing creation of new mappings. The format of mappings in all files is the same.