# Chapter 26 + Setting Up a Web Proxy with Squid 657

Edit the file to uncomment this line by removing # from it.

```
cache_dir ufs /var/cache/squid 100 16 256
```

If you try again, you may see a similar error message until you also add a line like this:

```
visible_hostname bibleserver.local.net
```

Search the file for visible_hostname. You will see where it is explained, but you will have to edit the file by hand and add it. Squid will not start until it knows what host name it is addressing.

Now if you try again, you will see that Squid is starting correctly:

```
rootproxy:/tmp# rcsquid start
Starting squid
```

If you look in /var/cache/squid/, you will see the cache directories have been created: The SUSE start script checks for their existence and creates them if necessary (so in fact you do not need to manually run squid -z as stated in Squid's own documentation).

![](bbox=[0.193, 0.506, 0.235, 0.563])

> Squid installs a considerable amount of documentation (including a fully commented configuration file) in the directory /usr/share/doc/packages/squid.

If you now list /var/cache/squid/, you see 16 directories 00, 01, 02, ..., 0F, each of 256 subdirectories 00, 01, ..., FF. So you will have a total of 4,096 directories in the cache directory structure. It is in that Squid saves copies of the objects that it projects. Clearly you could have these numbers by changing the values in the configuration file for cache_dir. You can stop Squid (rcsquid stop), remove these directories, and change the value of the cache_dir parameter to, for example:

```
cache_dir ufs /var/cache/squid 100 256 256
```

If you now start Squid, you find that there are 256 directories under /var/cache/squid with 256 subdirectories each.

If the rcsquid start command used earlier worked, you will probably want to force Squid to start at every boot by enabling it in the YaST runlevel editor, or by using the command insserv squid.

Squid runs by default on port 3128. This can also be changed in the configuration file (the other popular port for a proxy server is 8080). Now go to a client machine