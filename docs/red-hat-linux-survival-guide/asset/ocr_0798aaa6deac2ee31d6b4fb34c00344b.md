over many servers. The main idea is to share load among multiple servers of a kind, a practice typically used for balancing Web load over multiple Web servers. This trick is called round robin DNS.

Say that you have two Web servers, www1.yourdomain.com (192.168.1.10) and www2.yourdomain.com (192.168.1.20), and you would like to balance the load for the www.yourdomain.com on these two servers by using round robin DNS. In your yourdomain.com zone file add the following lines:

```
www1 IN A 192.168.1.10
www2 IN A 192.168.1.20
```

```
www IN CNAME www1
www IN CNAME www2
```

Restart your name server and ping the www.yourdomain.com host. You will see the 192.168.1.10 address in the ping output. Stop and restart pinging the same host, and now you'll see the second IP address being pinged. This is due to the fact that the preceding configuration tells the name server to cycle through the CNAME records for www. In other words, the www.yourdomain.com host is both www1.yourdomain.com and www2.yourdomain.com.

Now when someone enters www.yourdomain.com, the name server will give out the first address once, and then for the next request it will give out the second address and keep on cycling between these addresses.

One of the disadvantages of the round robin DNS trick is that there is no way for the name server to know which system is heavily loaded and which is not; it just blindly cycles. If one of the servers crashes or becomes unavailable for some reason, the round robin DNS will still return the broken server's IP on a regular basis. This can be quite chaotic because some people will be able to get to the sites and some won't.

If your load demands better management and it is important to check your server's health, your best choice is to get a hardware solution by using the new hardware products such as the Web Director (www.radware.com/), Ace Director (www.alteon.com/), or Local Director (www.cisco.com/).