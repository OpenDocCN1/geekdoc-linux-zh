# Interval between logging stats

This setting controls how often BIND writes general server statistics to the logs. By default this occurs every 60 minutes, and if set to 0 statistics logging will be turned off. This option correlates to the statistics-interval directive.

# Do full recursive lookups for clients?

BIND can respond in one of two ways if it does not have an answer for a client. If this option is set to Yes, the default, then BIND will perform the lookup itself on a parent or root server. If this is turned off, BIND will simply refer the client to another name server that can answer the query. This option configures the recursion directive.

# Allow multiple CNAME aliases for one name?

Older versions of BIND allowed multiple CNAME resource records for a single domain, and many sites used this for load balancing. However, this usage is against standards and is not recommended. Turning this on allows you to use multiple CNAMES, as in older versions of BIND. The default is off, and it correlates to the multiple-cnames directive.

# Fetch glue records?

If this option is set to Yes, the default, the server will fetch "glue" resource records it does not have when constructing the additional data section of a response. Setting this to No can be used in conjunction with recursion no to prevent the server's cache from growing or becoming corrupted. However, doing this increases the work for the client. This option configures the fetch-glue directive.

# Set authoritative AA bit on responses?

BIND normally caches negative responses (i.e., NXDOMAIN, or "this does not exist"), however, some very old servers and clients may have problems with this and generate errors. It's probably wise to upgrade those old clients and servers rather than turning this off. This option configures the auth-nxdomain directive and defaults to Yes.

# Control Interface Options

BIND provides a command-line utility called rndc (or rdc in older versions) that allows an administrator to perform some administrative tasks. The newer rndc version allows these tasks to be performed on remote BIND servers as well as a server running locally, as it operates via a network socket. Common uses for this utility include stopping the named process, forcing a reload of configuration files, refreshing zone information, and triggering a dump of server stats. Because the rndc tool can be used to shut down the server, as well as other potentially dangerous actions, its use should be limited to a few trusted client addresses.

This page of the BIND module provides access to the controls section of the BIND configuration file and configures the hosts that are allowed to connect to the running BIND server.