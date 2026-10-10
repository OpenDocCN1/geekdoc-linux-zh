The Squid proxy can also be used to filter individual sites so that users cannot access them. Suppose you do not want your users to access CNN.com or bbc.co.uk. The following lines will deny these sites:

```
```
acl newssites dstdomain .bbc.co.uk .cnn.com
http_access deny newssites
```
```

You can be more specific about when you allow or deny access to a site; for instance, you may allow the users to access the domains in the “newssites” group specified above during the lunch hour. For this, add a new acl, and the configuration file should look like that given below:

```
```
acl newssites dstdomain .bbc.co.uk .cnn.com
acl lunchtime MTWHFAS 12:00 13:00
http_access allow newssites lunchtime
http_access deny newssites
```
```

Note that the specification of the days of the week is Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, and Sunday. When Squid matches a line in the configuration file for http access, it will execute this and stop reading the file. The order of the lines is therefore important. Obviously, the more rules you require, the more complex the file will become. Often, used rules should therefore come at the beginning of the file whenever possible, to speed up execution. You can also block certain IP addresses or groups of addresses or allow full access for certain IP addresses, such as servers.

# ## Exam Warning

Squid can be used as a proxy server and as a caching server. When it is a caching server, it displays data to the client that has already in its cache; for example, a Web page. When it is used as a proxy, it is acting as a go-between for requests from a client to the target server. The target server will therefore not be able to communicate directly with the client.

# # APPLICATION SERVICES

The final section in this chapter will look at the application services that can be installed and run on a server. The main application services that are required by most companies are examined – namely printing, mail, and a database. These application services should not be confused with the client’s view of these, who can have a local printer and an electronic mail (e-mail