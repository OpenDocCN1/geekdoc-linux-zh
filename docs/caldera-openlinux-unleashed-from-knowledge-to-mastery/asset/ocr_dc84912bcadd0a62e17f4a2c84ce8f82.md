# PART II

As mentioned previously, a cache may not even be suitable if the majority of external connections go out to particularly dynamic Internet resources. The benefits of caching in such cases may be meager.

Once you have decided that Squid is for you (and you would certainly be following in the footsteps of many large installations and ISPs if you did so), you have to deal with building and installing it. (It doesn't come with the default OpenLinux). This is another package that uses autoconf, so it is relatively simple to get going (though there are some advanced options you need to be aware of).

Before installing Squid, you need to seriously consider how many clients will be using your cache and plan your hardware and installation requirements around that. For 5 to 10 workstations, 64 to 128MB of RAM and a gig of disk space should do well in improving your Web surfing experience. The hardware requirements can grow to tremendous proportions as you add users, however, and putting a lot of people behind a too-small cache is likely to slow down access to the Internet rather than speed it up.

A major part of a caching proxy server system is the configuration and management of large disk quantities, sometimes in the 10- to 20-gigabyte range of space for large local area networks. Without a solid understanding of disk hardware management, the task of setting up Squid could be difficult. The simplest implementation would be an assignment (in squid.conf) of all caching to one disk, but this results in the presence of a physical choke point as many users try to access that disk.

For large disk systems, even using RAID, Squid allows assignment of multiple caches across that disk real estate in a wide variety of configuration options.

By default, the software installs to `/usr/local/squid`. If you have a particular place with more space and faster disks, you can set that by invoking *configure* as

```
$ ./.configure --prefix=/path/to/squid*
```

Some other *configure* options you might want to set are as follows:

+   - **-enable-gnuregexp**     Compiles GNUregexp, a purportedly superior Regular Expression library for Squid to use.

+   - **-enable-icmp**       Enables ICMP pinging. This feature allows Squid to map other caches and destination sites to determine which cache is the closest from which to retrieve cached data, or whether it should retrieve the URL directly.

+   - **-enable-delay-pools**  Enables delay pools to limit bandwidth usage. This can be used as a type of “traffic shaper”; that is, it can effectively limit the bandwidth of client computers to a pre-determined amount.