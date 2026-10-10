![](bbox=[0.1, 0.09, 0.93, 0.28])

Figure 4.7: screenshot

The test.php file was served by the CentOS 6.4 server.

We will go ahead and edit the nginx.conf file again (see Figs. 4.8 and 4.9).

```
```
upstream app_rack {
    #ip_hash;
    server 10.0.2.13:8080 max_fails=3 fail_timeout=30s;
    server 10.0.2.14:8080 weight=3;
    # backup can only be used if ip_hash is not present
    server 127.0.0.1:8080 down;
}
```
```

Figure 4.8: The requests will be served by either the Debian or the CentOS server

```
```
upstream app_rack {
    #ip_hash;
    server 10.0.2.13:8080 down; # max_fails=3 fail_timeout=30s;
    server 10.0.2.14:8080 weight=2 down;
    # backup can only be used if ip_hash is not present
    server 127.0.0.1:8080 backup;
}
```
```

Figure 4.9: Since The Debian and CentOS servers have marked as down, all the requests will be forwarded to the local Ubuntu 12.04 server

With the upstream block show in Fig. 4.9, the php file will be served by the Ubuntu server (see Fig. 4.10)