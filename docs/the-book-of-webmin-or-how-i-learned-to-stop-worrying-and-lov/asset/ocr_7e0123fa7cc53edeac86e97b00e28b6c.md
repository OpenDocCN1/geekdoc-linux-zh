> **CAUTION** *It is a very common mistake to raise the above two options to extreme levels when performance of an Apache installation seems sluggish. It is very rarely actually the source of the problem, but it seems a popular first reaction among new Apache administrators. Tuning Apache for performance is well documented in a number of locations, and much documentation about tuning for specific OS platforms is also available on the Internet. A good place to start is the Apache Performance Notes page [http://httpd.apache.org/docs/misc/perf-tuning.html]. The documentation found there will address nearly all performance issues that most users will ever run into.*

# Initial server processes

The number of child processes that are spawned when the httpd is started. Correlates to the StartServers [http://www.apache.org/docs/mod/core.html#startservers] directive and defaults to 5. This usually does not need to be modified, except on high load servers.

# Display extended status information

If the status module is enabled on the server, turning this on will keep track of extended status information for each request and present them in a web page or machine readable format. This option edits the s ExtendedStatus [http://httpd.apache.org/docs/mod/mod_status.html] directive. This option requires the mod_status module to be loaded.

> **NOTE** *To access the extended status information from a running Apache server, you can browse to the address [http://www.yourdomain.com/server-status]. Note that access control should generally be configured to tightly restrict access to this URL, as it may contain sensitive data about your web server environment.*

The information provided by mod_status, with extended status enabled, includes statistics about the number of child processes and the number of connected clients, the average number of requests per second being served, the average number of bytes per request, and the current CPU percentage being used by each Apache process. A machine readable form of this data may be collected from [http://www.yourdomain.com/server-status?auto]. The latter is ideal for use in scripts to gather statistics from your server automatically.

> **CAUTION** *Because of the persistent nature of this type of data, this module is only functional when Apache is run in standalone mode, and not when run in inetd mode. Because of the large number of problems involved in running Apache under inetd, and problems inherent to inetd, it is simply best to avoid inetd altogether, anyway.*

# Networking and Addresses

This section is for configuring the network addresses and ports where Apache will listen, and some other access limits, timeouts, and queue options (Figure 7-2).