# # Part IV Networking

The http_port tag identifies the port on which Squid listens for HTTP client requests. The default port to use is 3128. Optionally, you can add a hostname (e.g., example.com:3128) or IP address (e.g., 10.0.0.1:3128) to limit allowed incoming requests to those made to a particular hostname or IP address.

```
hierarchy_stoplist cgi-bin ?
```

The hierarchy_stoplist tag indicates that when a certain string of characters appears in a URL, the content should be obtained from the original server and not from a cache peer. In this example, requests for the string cgi-bin and the question mark character (?) are all forwarded to the originating server.

```
acl QUERY urlpath regex cgi-bin ?
cache deny QUERY
```

The preceding two lines can be used to cause URLs containing certain characters to never be cached. These go along with the previous line by not caching URLs containing the same strings (cgi-bin and ?) that are always sought from the original server.

```
acl apache rep_header Server "Apache"
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

The acl tags are used to create access control lists. The first line in the preceding code creates an access control list called apache and assigns any response headers containing Server : Apache to the apache acl. After that, the all acl is defined to include all IP addresses. The next acl line assigns the manager acl to handle the cache_object protocol. The localhost source is assigned to the IP address of 127.0.0.1.

```
access_log /var/log/squid/access.log squid
```

The preceding line identifies the location of the Squid access.log file. As the name implies, this file contains messages about requests to access the Squid server.

Squid includes default settings for how long different types of content in cache are still considered to be fresh. The following refresh_pattern values are included in the squid.conf file:

```
refresh_pattern   -ftp:    1440     20%    10080
refresh_pattern   -gopher:  1440     0%     1440
refresh_pattern   .        0        20%    4320
```

In the code just shown, all lines that begin (') with ftp or gopher are set to expire in 1,440 minutes. The percentage of the object's age during which it is considered to be fresh is shown in the next column (20%, 0%, and 20%). The last column indicates the maximum number of