
the parent, it can probably service that request without making another request to the original server. This hierarchy also supports *sibling caches*, which can, in effect, create a pool of caching servers on the same level.

> **CAUTION:** Caching can consume a lot of your hard disk space if you let it. If you have separate partitions on your system, make sure that you have enough space in `/var` to handle the added load.

Here are some cache-related tags that you should consider setting:

- `cache_peer` — If there is a cache parent whose resources you can use, you can add the parent cache using this tag. You would need to obtain the parent cache's hostname, the type of cache (parent), the proxy port (probably 3128), and the ICP port (probably 3130) from the administrator of the parent cache. (If you have no parent cache, you don't have to set this value.) Here's an example of a `cache_peer` entry:
  ```
  cache_peer parent.hansonhistory.com parent 3128 3130
  ```
  You can also add options to the end of the line, such as proxy-only (so that what you get from the parent isn't stored locally) and weight=n (where n is replaced by a number above 1 to indicate that the parent should be used above other parents). Add default if the parent is used as a last resort (when all other parents don't have the requested data).

- `cache_mem` — Specifies the amount of cache memory (RAM) used to store in-transit objects (ones that are currently being used), hot objects (ones that are used often), and negative-cached objects (recent failed requests). The default is 8MB, although you can raise that value. To set `cache_mem` to 16MB, enter the following:
  ```
  cache_mem 16 MB
  ```
  > **NOTE:** Because Squid will probably use a total of three times the amount of space you give it for all its processing, Squid documentation recommends that you use a `cache_mem` one-third the size of the space that you actually have available for Squid.

- `cache_dir` — Specifies the directory (or directories if you want to distribute cache across multiple disks or partitions) in which cache swap files are stored. The default is the `/var/spool/squid` directory. You can also specify how much disk space to use for cache in megabytes (100 is the default), the number of first-level directories to create (16 is the default), and the number of second-level directories (256 is the default). Here's an example:
  ```
  cache_dir ufs /var/spool/squid 100 16 256
  ```
  > **NOTE:** The cache directory must exist. Squid won't create it for you. It will, however, create the first- and second-level directories.

- `cache_mgr` — Add the e-mail address of the user who should receive e-mail if the cache daemon dies. By default, e-mail is sent to root. To explicitly set `cache_mgr` to the root user, use the following:
  ```text
  cache_mgr root
  ```

- `cache_effective_user` — After the squid daemon process is started as root, subsequent processes are run as `squid` user and group (by default). To change that subsequent user to a different name (for example, to `nobody`) set the `cache_effective_user` as follows:
  ```text
  cache_effective_user nobody
  ```
  > **NOTE:** When I changed the `cache_effective_user` name so that a user other than `squid` ran the `squid` daemon, the `messages` log recorded several failed attempts to initialize the Squid cache before the process exited. When I changed the user name back to `squid`, the process started properly. To use the `cache_effective_user` feature effectively, you must identify which files are not allowing access.

## Configuring port numbers in squid.conf

When you configure client software to use your Squid proxy services, the clients need to know your computer's name (or IP address) and the port numbers associated with the services. For a client wanting to use your proxy to access the Web, the HTTP port is the needed number. Here are the tags that you use to set port values in Squid for different services, along with their default values:

- `http_port 3128` — The `http_port` is set to 3128 by default. Client workstations need to know this number (or the number you change this value to) to access your proxy server for HTTP services (that is, Web browsing).
- `icmp_port 3130` — ICP requests are sent to and from neighboring caches through port 3130 by default.
- `htcp_port 4827` — ICP sends HTCP requests to and from neighboring caches on port 4827 by default.

## Debugging Squid

If Squid isn’t working properly when you set it up, or if you just want to monitor Squid activities, there are several tools and log files to help you.

### Checking the squid.conf file

By running the squid daemon with the `-X` option (described earlier), you can check what is being set from the `squid.conf` file. You can add an `-X` option to the `SQUID_OPTS` line in the `/etc/sysconfig/squid` file. Then run `service squid restart`. A whole lot of information is output, which details what is being set from `squid.conf`. If there are syntax errors in the file, they appear here.

### Checking Squid log files

Squid log files (in Fedora) are stored in the `/var/log/squid` directory by default. The following are the log files created there, descriptions of what they contain, and descriptions of how they might help you debug potential problems:

- `access.log` — Contains entries that describe each time the cache has been hit or missed when a client requests HTTP content. Along with that information is the identity of the host making the request (IP address) and the content they are requesting. Use this information to find out when content is being used from cache and when the remote server must be accessed to obtain the content. The following are possible access result codes:
  - `TCP_DENIED` — Squid denied access for the request.
  - `TCP_HIT` — Cache contained a valid copy of the object.
  - `TCP_IMS_HIT` — A fresh version of the requested object was still in cache when the client asked if the content had changed.
  - `TCP_IMS_MISS` — An If-Modified-Since request was issued by the client for a stale object.
  - `TCP_MEM_HIT` — Memory contained a valid copy of the object.
  - `TCP_MISS` — Cache did not contain the object.
  - `TCP_NEGATIVE_HIT` — The object was negatively cached, meaning that an error was returned (such as the file not being found) when the object was requested.
  - `TCP_REF_FAIL_HIT` — A stale object was returned from cache because of a failed request to validate the object.
  - `TCP_REFRESH_UNMODIFIED` — A stale copy of the object was in cache, but a request to the server returned information that the object had not been modified.
  - `TCP_REFRESH_MODIFIED` — A stale cache object was replaced by new, updated content.
  - `TCP_SWAPFAIL` — An object could not be accessed from cache, despite the belief that the object should have been there.
- `cache.log` — Contains valuable information about your Squid configuration when the squid daemon starts up. You can see how much memory is available (Max Mem), how much swap space (Max Swap), the location of the cache directory (/var/spool/squid), the types of connections being accepted (HTTP, ICP, and SNMP), and the port on which connections are being accepted. You can also see a lot of information about cached objects (such as how many are loaded, expired, or canceled).
- `store.log` — Contains entries that show when content is being swapped out from memory to the cache (SWAPOUT), swapped back into memory from cache (SWAPIN), or released from cache (RELEASE). You can see where the content comes from originally and where it is being placed in the cache. Time is logged in this file in raw UNIX time (in milliseconds).

You might also be interested in another log file: /var/log/messages. This file contains entries describing the startup and exit status of the squid daemon.

### Using the top command

Run the top command to see information about running processes, including the Squid process. If you are concerned about performance hits from too much Squid activity, type M from within the top window. The M option displays information about running processes, sorted by the percent of memory each process is using. If you find that Squid is consuming too large a percentage of your system memory, you can reduce the memory usage by resetting the cache_mem value in your squid.conf file.

## Setting Up Proxy Clients

For your Linux proxy server to provide Web-browsing access (HTTP) to the Windows and Linux client computers on your network, each client needs to do a bit of setup within the Web browser. The beauty of using proxy servers is in what your client computers don't need to know, such as the following:

- Addresses of DNS servers
- Telephone numbers of ISPs
- Chat scripts to connect to the ISP
