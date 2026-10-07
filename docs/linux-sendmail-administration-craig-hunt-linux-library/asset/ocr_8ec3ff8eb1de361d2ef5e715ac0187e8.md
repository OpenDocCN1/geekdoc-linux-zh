FEATURE (dnsbl1) Controls mail delivery based on a DNS blacklist. Source addresses and destination addresses listed in the DNS database may be denied mail delivery or relay services.

FEATURE(promiscuous_relay) Relays mail from any site to any site. Normally, Sendmail does not relay mail. Using this feature is a bad idea because it makes you a possible relay service for spammers.

FEATURE(relay_entire_domain) Relays mail from any domain defined in class M to any site.

FEATURE(relay_hosts_only) Relays mail from any host defined in the access database or class R.

FEATURE(relay_based_on_MX) Relays mail from any site for which your system is the MX server.

FEATURE(relay_local_from) Relays mail with a sender address that contains your local domain name.

WARNING Mail relays can be abused by spammers and spoofers. Use them with caution.

Inbound mail can also be filtered to reduce the impact of spammers. Two macros are available for this purpose:

MAIL_FILTER(`name`, `equates`) This macro defines a mail filter using the Sendmail Mail Filter API syntax.

INPUT_MAIL_FILTER(`name`, `equates`) This macro defines a mail filter and sets up the call for that mail filter.

The DOM source file is also used for features and macros that directly relate to DNS. These features are:

FEATURE(accept_unqualified_senders) This feature accepts mail from the network even if the sender address does not include a hostname. Normally, only mail from a user directly logged on to the system is accepted without a hostname. This is a dangerous feature that should be used only on an isolated network.

FEATURE(accept_unresolvable_domains) This feature accepts mail from hostnames that cannot be resolved by DNS. This is a dangerous feature that is used only on systems that lack full-time DNS service.