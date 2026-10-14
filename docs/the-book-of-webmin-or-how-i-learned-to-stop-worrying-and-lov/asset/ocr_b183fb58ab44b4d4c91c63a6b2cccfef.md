# Proxy authentication realm

The realm that will be reported to clients when performing authentication. This option usually defaults to Squid proxy-caching web server, and correlates to the proxy_auth_realm directive. This name will likely appear in the browser popup window when the client is asked for authentication information.

# Cache manager email address

The email address of the administrator of this cache. This option corresponds to the cache_mgr directive and defaults to either webmaster or root on RPM-based systems. This address will be added to any error pages that are displayed to clients.

# Visible hostname

The host name that Squid will advertise itself on. This effects the host name that Squid uses when serving error messages. This option may need to be configured in cache clusters if you receive IP-forwarding errors. This option configures the visible_hostname.

# Unique hostname

Configures the unique_hostname directive, and sets a unique host name for Squid to report in cache clusters in order to allow detection of forwarding loops. Use this if you have multiple machines in a cluster with the same visible hostname.

# Cache announce host, port, and file

The host address and port that Squid will use to announce its availability to participate in a cache hierarchy. The cache announce file is simply a file containing a message to be sent with announcements. These options correspond to the announce_host, announce_port, and announce_file directives.

# Announcement period

Configures the announce_period directive, and refers to the frequency at which Squid will send announcement messages to the announce host.

# Miscellaneous Options

Miscellaneous Options is just what it sounds like: a hodgepodge of options that don't seem to fit anywhere else. Here you'll find several memory-related options, options regarding headers and user agent settings, and the powerful HTTP accelerator options (Figure 12-18).

# Startup DNS test addresses

This should point to a number of hosts that Squid can use to test whether DNS service is working properly on your network. If DNS isn't working properly, Squid will not be able to service requests, so it will refuse to start, with a brief