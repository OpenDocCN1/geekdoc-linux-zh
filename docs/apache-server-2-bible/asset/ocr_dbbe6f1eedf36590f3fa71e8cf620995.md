![](bbox=[0.15, 0.13, 0.85, 0.44])

Figure 22-4: An improved Web network

# Balancing load using the DNS server

The idea is to share the load among multiple servers of a kind. This typically is used for balancing the Web traffic over multiple Web servers. This trick is called round-robin Domain Name Service.

Suppose that you have two Web servers, www1.yourdomain.com (192.168.1.10) and www2.yourdomain.com (192.168.1.20) and you want to balance the load for www.yourdomain.com on these two servers using the round-robin DNS trick. Add the following lines to your yourdomain.com zone file:

```
```
www1    IN    A    192.168.1.10
www2    IN    A    192.168.1.20

www     IN    CNAME    www1
www     IN    CNAME    www2
```
```

Restart your name server and ping the www.yourdomain.com host. You will see the 192.168.1.10 address in the ping output. Stop and restart pinging the same host, and you'll see the second IP address being pinged, because the preceding configuration tells the name server to cycle through the CNAME records for www. In other words, the www.yourdomain.com host is both www1.yourdomain.com and www2.yourdomain.com.

Now, when someone enters www.yourdomain.com, the name server gives out the first address once, then gives out the second address for the next request, and keeps cycling between these addresses.