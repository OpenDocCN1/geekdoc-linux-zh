Not all transactions can take advantage of the persistent connections. A requirement for a persistent connection is that the resources being transmitted must have a known size. Because many CGI scripts, SSI commands, and other dynamically generated contents do not have a known length before transmission, they are unable to take advantage of this feature.

# KeepAlive

The KeepAlive directive enables you to activate/deactivate persistent use of TCP connections in Apache.

+   - Syntax: KeepAlive On | Off
+   - Default setting: KeepAlive On
+   - Context: Server config

Older Apache servers (prior to version 1.2) may require a numeric value instead of On/Off when using KeepAlive This value corresponds to the maximum number of requests you want Apache to entertain per request. A limit is imposed to prevent a client from taking over all your server resources. To disable KeepAlive in the older Apache versions, use 0 (zero) as the value.

# KeepAliveTimeout

If you have the KeepAlive directive set to on, you can use the KeepAliveTimeout directive to limit the number of seconds Apache will wait for a subsequent request before closing a connection. After a request is received, the timeout value specified by the Timeout directive applies.

+   - Syntax: KeepAliveTimeout seconds
+   - Default setting: KeepAliveTimeout 15
+   - Context: Server config

# MaxKeepAliveRequests

The MaxKeepAliveRequests directive limits the number of requests allowed per connection when KeepAlive is on. If it is set to 0 (zero), unlimited requests will be allowed. I recommend that this setting be kept to a high value for maximum server performance.

+   - Syntax: MaxKeepAliveRequests number
+   - Default setting: MaxKeepAliveRequests 100
+   - Context: Server config