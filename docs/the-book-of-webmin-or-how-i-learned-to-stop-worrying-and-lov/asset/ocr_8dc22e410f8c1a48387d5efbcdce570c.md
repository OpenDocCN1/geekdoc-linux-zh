# Cache metadata file

Filename used in each store directory to store the web cache meta data, which is a sort of index for the web cache object store. This is not a human-readable log, and it is strongly recommended that you leave it in its default location on each store directory, unless you really know what you’re doing. This option correlates to the cache_swap_log directive.

# Use HTTPD log format

Allows you to specify that Squid should write its access.log in HTTPD common log file format, such as that used by Apache and many other web servers. This allows you to parse the log and generate reports using a wider array of tools. However, this format does not provide several types of information specific to caches and is generally less useful when tracking cache usage and solving problems. Because there are several effective tools for parsing and generating reports from the Squid standard access logs, it is usually preferable to leave this at its default of being off. This option configures the emulate_httpd_log directive. The Calamaris cache access log analyzer does not work if this option is enabled.

# Log MIME headers

Provides a means to log extra information about your requests in the access log. This causes Squid to also write the request and response MIME headers for every request. These will appear in brackets at the end of each access.log entry. This option correlates to the log_mime_hdrs directive.

# Perform RFC931 ident lookups for ACLs

Indicates which of the Access Control Lists that are defined should have ident lookups performed for each request in the access log. Because of the performance impact of using this option, it is not on by default. This option configures the ident_lookup_access directive.

# RFC931 ident timeout

The timeout, usually in seconds, for ident lookups. If this is set too high, you may be susceptible to denial of service from having too many outstanding ident requests. The default for this is 10 seconds, and it applies to the ident_timeout directive.

# Log full hostnames

Configures whether Squid will attempt to resolve the host name, so the fully qualified domain name can be logged. This can, in some cases, increase latency of requests. This option correlates to the log_fqdn directive.