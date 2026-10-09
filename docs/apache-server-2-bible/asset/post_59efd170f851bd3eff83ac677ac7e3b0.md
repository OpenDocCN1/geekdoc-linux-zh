
Determine a goal for your server. Make an estimate (or guess) of how many requests you want to be able to service from your Web server. Write it down in a goal statement such as, “I wish to service $N$ requests per second.”

Restart your Web server and from a system other than the Web server, run the ab command as follows:

```
./ab -n number_of_total_requests \
   -c number_of_simultaneous_requests \
      http://your_web_server/page
```

For example:

```
./ab -n 1000 -c 50 http://www.domain.com/
```

The ApacheBench tool will make 50 concurrent requests and a total of 1,000 requests. Sample output is shown below:

```
Server Software:        Apache/2.0.16
Server Hostname:        localhost
Server Port:            80

Document Path:          /
Document Length:        1311 bytes

Concurrency Level:      50
Time taken for tests:   8.794 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      1754000 bytes
HTML transferred:       1311000 bytes
Requests per second:    113.71
Transfer rate:          199.45 kb/s received

Connection Times (ms)
              min     avg     max
Connect:        0      0       5
Processing:   111   427     550
Total:        111   427     555
```

Notice that Requests per second is 113.71 for accessing the home page of the http://www.domain.com site. Change the concurrent request count to a higher number and see how the server handles additional concurrent load.

Now change the values for the MaxClients, ThreadsPerChild, MaxThreadsPerChild, and so on based on your MPM, restart Apache, and apply the same benchmark tests by using ab as before. You should see your Requests per second go up and down based on numbers you try. As you tweak the numbers by changing the directive values, make sure you record the values and the performance so that you can determine what is a good setting for you.

# Caching for Speed

Caching Web contents is not a new concept. Most busy Web sites implement caching by using proxy servers or another mechanism. Here I discuss two options from which you can choose. You should also look into the proxy capabilities of Apache by using the `mod_proxy` module discussed in Chapter 10.

# Caching frequently used files in memory with mod_fcache

The `mod_fcache` module for Apache caches a given file type in memory. The cached files are stored in the server’s main memory space and are accessible to all the Apache child processes. You can download this module from www.fractal.net/mod_fcache.tm. To compile and install this module, follow these steps:

- As root, extract the module source by using the `tar xvfz mod_fcache.tar.gz` command and copy the newly created directory to the modules subdirectory of your Apache source distribution. For example, if you have installed Apache source in `/usr/local/src/httpd_2.0.16` and `fcache` in `/usr/local/src/fcache`, then you can copy the module files using `cp -r /usr/local/src/fcache /usr/local/src/httpd_2.0.16 modules` command.
- Change the directory to the `modules/fcache` subdirectory of the Apache source distribution. Take a look at the `config.m4` file and see if anything needs to be changed for your system. Most likely you do not have to make any changes. If you do, you should know who you are.
- Run `autoconf` to configure everything.
- Change the directory back to the top-level Apache source distribution and run the Apache `configure` script with all the options you normally use (see `config.status` file) and the `--enable-fcache` option.
- Compile and install Apache as usual using `make && make install` command.
- Restart the Apache Web server by using the `/usr/local/httpd/apachectl restart` command.

Now you are ready to use this module. To cache GIF images that are served from a directory called `common_images`, for example, you use the following configuration segment in `httpd.conf`:

```
<Directory /common_images>
  fcache              On
  fcache_CacheTypes   image/gif
  fcache_MaxSize      10240
  fcache_RecomputeTables 600
</Directory>
```

Some things to note about the above segment:

- `fcache` turns on the caching module.
- `fcache.CacheTypes` directive sets the MIME type for caching. The sample configuration sets this to `image/gif`. If you wish to cache all types of images, you can use `image/*` instead.
- `fcache.MaxSize` sets the `size` of the cache. Here the memory cache is set to 10MB (1024KB × 10). Remember that you must have plenty of memory to cache files.
- `fcache.RecomputeTables` directive sets the time in seconds to recompute the cache tables. The default of 10 minutes is sufficient for most purposes.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_651_0.png)

To view cache statistics, you can create the following configuration:

```
<Location /fcache-stats>
SetHandler fcache-stats-handler
</Location>
```

and then go to the http://your_web_server/fcache-stats page.

# Getting slick with the Squid proxy-caching server

Squid is an open-source HTTP 1.1-compliant proxy-caching server that you can use to enhance your users’ Web-browsing experience. You can download the latest stable Squid source distribution from www.squid-cache.org.

Ideally, you want to run the proxy-caching server with two network interfaces. One interface connects it to the Internet gateway or the router and the other one connects it to the internal network.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_651_1.png)

Disabling IP forwarding on the proxy-caching system ensures that no one can bypass the proxy server and access the Internet directly.

The following sections discuss installing and configuring Squid.

# Compiling and installing Squid proxy-caching server

To compile and install Squid, follow these steps:

1. As root, extract the source distribution using the `tar xvfz squid-version.tar.gz` (where *version* is the latest version number of the Squid software).
2. Run the `./configure --prefix=/usr/local/squid` command to configure Squid source code for your system.
3. Run `make all; make install` to install Squid in `/usr/local/squid` directory.

After you have installed Squid, you need to configure it (see the next section).

# Configuring Squid

To configure Squid, follow these steps:

- Create a group called *nogroup* by using the `groupadd nogroup` command. This group will be used by Squid.
- Run the `chown -R nobody:nogroup /usr/local/squid` command to give the ownership of the `/usr/local/squid` directory and all its subdirectories to nobody user and to the group called nogroup. This enables Squid (running as *nobody* user) to create cache directories and files and to write logs. Modify the `/usr/local/squid/etc/squid.conf` file as discussed in the following steps.
- Decide which port you want to run the proxy-cache on. Because most sites run proxy-cache on 8080, I use this value here. Add the following line in `squid.conf`:

```
http_port 8080
```

This tells Squid to listen to port 8080 for proxy requests.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_652_0.png)

If you prefer a different port, use it here. Be sure not to use a port that is already in use by another server. Ideally, you want to use port numbers above 1024 to avoid collision with standard services, but if you know you are not running a Web server on port 80 and want to run your proxy-cache on that port, you can do so. Also, a quick way to check whether a port is available is to run `telnet localhost port_number` command where *port_number* is the port number you want to use for proxy-cache. If you get a connection failure message, the port is currently not in use.

- You need to define where you want to keep the cache data. Define the following line in the `squid.conf`:

```
cache_dir ufs /usr/local/squid/cache 100 16 256
```

This tells Squid that you want to store the cache data in `/usr/local/squid/cache`. If you have a very large user base that will use this proxy-cache, it is a very good idea to have multiple cache directories spanning different drives. This reduces drive I/O-related wait because multiple, independent drives are always faster than a single drive.

- Default Squid configuration does not allow any connection from anywhere; this is a security feature often known as "deny everyone, allow only those who should have access." So, you have to create an access control list (ACL) that enables your network to access to the proxy-cache. For example, if your network address is 192.168.1.0 with subnet 255.255.255.0, then you can define the following line in `squid.conf` to create an ACL for your network:

```
acl local_net src 192.168.1.0/255.255.255.0
```
