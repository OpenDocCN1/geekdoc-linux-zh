# # Debugging Squid

If Squid isn’t working properly when you set it up, or if you just want to monitor Squid activities, there are several tools and log files to help you.

# ## Checking the squid.conf file

By running the squid daemon with the `-X` option (described earlier), you can check what is being set from the `squid.conf` file. You can add an `-X` option to the `SQUID_OPTS` line in the `/etc/sysconfig/squid` file. Then run `service squid restart`. A whole lot of information is output, which details what is being set from `squid.conf`. If there are syntax errors in the file, they appear here.

# ## Checking Squid log files

Squid log files (in Fedora) are stored in the `/var/log/squid` directory by default. The following are the log files created there, descriptions of what they contain, and descriptions of how they might help you debug potential problems:

+   * `access.log` — Contains entries that describe each time the cache has been hit or missed when a client requests HTTP content. Along with that information is the identity of the host making the request (IP address) and the content they are requesting. Use this information to find out when content is being used from cache and when the remote server must be accessed to obtain the content. The following are possible access result codes:

+   	* `TCP_DENIED` — Squid denied access for the request.
+   	* `TCP_HIT` — Cache contained a valid copy of the object.
+   	* `TCP_IMS_HIT` — A fresh version of the requested object was still in cache when the client asked if the content had changed.
+   	* `TCP_IMS_MISS` — An If-Modified-Since request was issued by the client for a stale object.
+   	* `TCP_MEM_HIT` — Memory contained a valid copy of the object.
+   	* `TCP_MISS` — Cache did not contain the object.
+   	* `TCP_NEGATIVE_HIT` — The object was negatively cached, meaning that an error was returned (such as the file not being found) when the object was requested.
+   	* `TCP_REF_FAIL_HIT` — A stale object was returned from cache because of a failed request to validate the object.
+   	* `TCP_REFRESH_UNMODIFIED` — A stale copy of the object was in cache, but a request to the server returned information that the object had not been modified.