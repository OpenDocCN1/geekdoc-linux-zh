You can add any options, along with the `-D` option, between the quotes. Most of these options are useful for debugging Squid:

+   * `-a port#` — Substitute for port# a port number that will be used instead of the default port number (3128) for servicing HTTP proxy requests. This is useful for temporarily trying out an alternative port.
+   * `-f squidfile` — Use this option to specify an alternative `squid.conf` file (other than `/etc/squid/squid.conf`). Replace `squidfile` with the name of the alternative `squid.conf` file. This is a good way to try out a new `squid.conf` file before you replace the old one.
+   * `-d level` — Change the debugging level to a number indicated by `level`. This also causes debugging messages to be sent to `stderr`.
+   * `-x` — Use this option to check that the values are set properly in your `squid.conf` file. It turns on full debugging while the `squid.conf` file is being interpreted.

You can restart the Squid service by typing `/etc/init.d/squid restart`. While the squid daemon is running, there are several ways you can run the `squid` command to change how the daemon works, using these options:

+   * `squid -k reconfigure` — Causes Squid to again read its configuration file.
+   * `squid -k shutdown` — Causes Squid to exit after waiting briefly for current connections to exit.
+   * `squid -k interrupt` — Shuts down Squid immediately, without waiting for connections to close.
+   * `squid -k kill` — Kills Squid immediately, without closing connections or log files. (Use this option only if other methods don’t work.)

With the squid daemon ready to run, you now need to set up the `squid.conf` configuration file.

# ## Using a simple squid.conf file

You can use the `/etc/squid/squid.conf` file that comes with squid to get started. Though the file contains lots of comments, the actual settings in that file are quite manageable. The following paragraphs described the lines that are contained in the default `squid.conf` file:

```
hierarchy_stoplist cgi-bin ?
```

The `hierarchy_stoplist` tag indicates that when a certain string of characters appear in a URL, the content should be obtained from the original server and not from a cache peer. In this example, requests for the string `cgi-bin` and the question mark character (?) are all forwarded to the originating server.