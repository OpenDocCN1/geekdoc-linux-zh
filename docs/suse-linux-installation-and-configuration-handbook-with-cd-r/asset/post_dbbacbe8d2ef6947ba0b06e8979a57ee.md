
megabytes of the cache. A reasonable value for starters is 100 MB, but again, this depends on your network and amount of users who will be using the cache. The third option is the number of directories that squid will create under /var/squid/cache to store the caches object in. Squid creates a hierarchy of directories in its cache directory; using the default value of 16 is good enough. The last option is the number of directories that squid will create in each of the 16 directories it creates. You can think of it as a level 1 and level 2 of directories. Using 256 means that in each of the 16 directories, squid will create 256 directories inside it. Again, the defaults are good enough.

## Creating a Cache Hierarchy

A cache hierarchy is a process in which you have more than one proxy server running with a line of communication between them. Cache hierarchies enable you to connect a network of proxies together to achieve the fastest response possible.

A typical scenario for cache hierarchies is when a user requests a URL from your proxy. If your proxy does not have the page on local disk, it will go ahead and download it from the origin server. If your server is part of a cache hierarchy, it will proceed to ask the other proxies whether they have that URL cached or not. If they do, it downloads it from them and gives it to you; otherwise, it gets it from the origin server.

Caches in cache hierarchies are one of two types—a parent or a sibling. When a proxy fails to find a page in its local cache, it will first ask the sibling caches whether they have it or not. If none of the siblings have it, the server doesn't get the page itself; it asks the parent to get it. If the parent has it cached, it passes it down to your server; if not, it proceeds to ask other servers on its level for it or gets it itself. The whole process is very much like a tree—parents are siblings to each other but parents to their children and so on.

### Creating a Cache Hierarchy of Siblings

To have two or more proxies communicate together in a sibling fashion is quite easy. It just requires a few modifications to their configuration files.

Let's say that you have two proxy servers on your network and you want them to communicate together as siblings. The first server is called server1 and the second one is called server2. Here's what you would enter in each of the servers' configuration files:

- In server1:
```
cache_host server2.company.com sibling 3128 3130 proxy-only
```
- In server2:
```
cache_host server1.company.com sibling 3128 3130 proxy-only
```

That's it; now both servers will communicate together if they can't find a request in their caches. The cache_host parameter takes the name of the other server as the first option, followed by the sibling keyword. The third option is the HTTP port of the other proxy server followed by the ICP port. The ICP port is the port that the server uses to communicate with other servers. Finally, the last option, the proxy_only, tells squid not to keep a copy of the requested page so it doesn't have a duplicate on all the servers. This option virtually doubles the size of your cache because you never have more than one copy of a page in all the caches.

This setup is useful if you have a large network and need a big proxy but don't have the resources to invest in huge machines. You can just use more than one machine to create a virtually big cache server.

### Creating a Parent Cache

In big networks, you might have a big proxy server on a fast link, and other smaller ones that are used to take the load off that big server. The big server is a parent to the others. The smaller servers can be siblings to each other, and when they can't find a page in their cache, they can consult the big server for it.

Configuring the small servers to use a parent cache is not much different from the sibling configuration. The only difference is that you don't perform any configuration to the parent server.

Say you have one big parent server called parent, and you want your server to use it when it fails to find a request. The configuration file of your server would include this entry:

```
cache_host parent.company.com parent 3128 3130
```

There, now your server will query the parent server for the request. But before it does that, it will first send packets to that server to check whether it's online or not. If you are sure that the parent always will be online, you can have squid skip that step:

```
cache_host parent.company.com parent 3128 3130 no-query default
```

The no-query option tells squid not to query for the server, to just use it. As for the default tag, that's another story.

You can have more than one parent server. Your server would ask each one whether it had the page or not. If none of the parents had the page, your server would ask the default server to get the page for it. Usually the default server is the one that your server will ask to get the page. You usually would choose the fastest server as the default server.

## Troubleshooting

*When I attempt to connect to the proxy server, I get an access denied message.*

The most common reason behind such a message is that the access rules are denying your access to the server or to the request that you made. Check your ACLs and http_access rules.

*I am having problems connecting to Hotmail from the proxy server; I get the error Intrusion Logged, Access Denied.*

This is because Hotmail requires that all connections be made from the same IP. To fix that, add the line

```
hierarchy_stoplist hotmail.com
```

to your squid.conf file.

*I get an error message saying Too many files open.*

This probably means that you are running out of file descriptors. To open a file, you need a file descriptor, and if you run out of them, you can't open new files. You can fix this by increasing the number of file descriptors on your system by typing the following command:

```
# echo 4024 > /proc/sys/fs/file-max
```

*I want to ban a long list of sites, but putting them all on the same ACL statement is a pain. Any ideas?*

Yes, just put them all in a file, with each on a line of its own. Then pass the name of the file to the ACL.

## Connectivity to the Internet

### In this chapter

- A Briefing on Connectivity to the Internet 406
- Connectivity Using Modems 406
- Serial Ports and Linux 408
- Setting Up a New Modem 408
- Modem Connection Software Requirements 408
- Configuring the Modem 409
- Configuring the Serial Port 414
- Telling YaST Where the Modem Is 416
- Establishing Your Connection 417
- Testing an Existing Connection 428
- General Modem Connection Troubleshooting 429
- Connectivity Using ISDN 431
- ISDN and Linux 432
- ISDN Connection Software Requirements 433
- Configuring the ISDN Card 434
- Configuring ISDN Hardware via YaST 434
- Other ISDN Configurations 436
- Configuring the ISDN Network Interface via YaST 437
- Setting Up a Nameserver via YaST 440
- General ISDN Troubleshooting 440
- MSN Format 441

## A Briefing on Connectivity to the Internet

When we talk about connectivity to the Internet, we actually talk about a whole generation. For in the previous 10 years, the Internet has become a way of life, a must-know technology, a profession, and much more. Connectivity to the Internet can be achieved through many methods. Using a modem or ISDN stand are the most common ones. Linux supports both. In this chapter we are going to discuss how to connect to the Internet using these dial-up services.

## Connectivity Using Modems

The modem has long since been known as the main device to connect computers to the Internet. Despite the proliferation of other connectivity devices, modems are still widely used in most countries. One reason for this is that many countries lack ISDN support. Even if the phone company supports ISDN, many ISPs do not support it.

## Using a Modem to Connect to the Internet

What do you need in order to set up Internet connectivity using modems on Linux?

- A modem, of course
- An Internet account
- A serial port
- PPP/SLIP support
- YaST setup
- PPP daemon

## What Is a Modem?

Modems are devices that can be used to transfer digital signals over phone lines that do not support digital signals. What you actually do when dialing up your ISP is dial to an existing modem at the ISP that is waiting for your call. Your modem converts the digital signal to an analog signal and sends it through the phone line to the other modem. The other modem converts the signal back to digital and feeds it to the server to which you're connecting. When the other modem sends you data, the roles swap. Therefore, a modem is a device that is used to transport digital data over an analog phone line by first converting it to analog and then restoring it back to digital.

## Types of Modems

Modems come in two basic types—internal and external. The significant difference between the two is that internal modems are built into either the motherboard or normal ISA/PCI
