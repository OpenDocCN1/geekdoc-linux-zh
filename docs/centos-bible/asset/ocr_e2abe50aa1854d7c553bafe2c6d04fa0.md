+   * `store.log` — Contains entries that show when content is being swapped out from memory to the cache (`SWAPOUT`), swapped back into memory from the cache (`SWAPIN`), or released from the cache (`RELEASE`). You can see where the content comes from originally and where it is being placed in the cache. Time is logged in this file in raw UNIX time (in milliseconds).

You might also be interested in another log file: `/var/log/messages`. This file contains entries describing the start-up and exit status of the `squid` daemon.

# Using the `top` Command

Run the `top` command to see information about running processes, including the `Squid` process. If you are concerned about performance hits from too much `Squid` activity, type `M` from within the top window. The `M` option displays information about running processes, sorted by the percent of memory each process is using. If you find that `Squid` is consuming too large a percentage of your system memory, you can reduce the memory usage by resetting the `cache_mem` value in your `squid.conf` file.

# Setting Up Proxy Clients

For your `Linux` proxy server to provide Web-browsing access (HTTP) to the `Windows` and `Linux` client computers on your network, each client needs to do a bit of setup within the Web browser. The beauty of using proxy servers is in what your client computers don't need to know, such as the following:

+   * Addresses of `DNS` servers
+   * Telephone numbers of `ISPs`
+   * Chat scripts to connect to the `ISP`

There are probably other things that clients don't need to know, but you get the idea. After the proxy server has a connection to the Internet and has allowed a client computer on the LAN access to that service, all the client needs to know is the following:

+   * **Hostname** — The name or IP address of the proxy server. This assumes that the client can reach the proxy over the `LAN` or other IP-based network.
+   * **Port Numbers** — The port number of the `HTTP` service (3128 by default). That same port number can be used for `FTP` service as well.

How you go about setting up proxy service on the client has more to do with the browser you are using than with the operating system you are using. Follow the procedures outlined in the following sections for setting up `Firelox`, `Microsoft Internet Explorer`, `Mosaic`, or `Lynx` browsers.