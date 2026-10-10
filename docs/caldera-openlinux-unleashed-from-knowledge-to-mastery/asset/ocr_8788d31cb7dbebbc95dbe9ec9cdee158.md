cache_peer | If you intend to have your cache interact with other caches (this is explained later chapter), you need to set this. An example line might be:
```
# host name type foo.net
# cache_peer parent.foo.net
# parent 3128 3130 [proxy only]
cache_peer sib1.foo.net
# sibling 3128 3130 [proxy only]
```

acl QUERY urlpath \n~regex cgi bin (? \nno_cache deny QUERY | These two lines define an ACL (Access Control List) that disallows caching of dynamic content.

cache_mem | This is the ideal amount of memory to use for object caching. This is not an upper bound on the total amount of memory that Squid can use. A good number for this is 1/3 to 1/2 of your physical memory for a dedicated Squid cache.

maximum_object_size | Largest object that squid will cache.

cache_dir | This sets the path to the cache directory, the maximum size to which the cache will grow in that directory, and the number of first and second level directories to create to store the cache, as follows:
[cacheDir] [size] [level1] [level2]

client_netmask | Determines the accuracy of IP logging. Set to 255.255.255.255 and the exact IP of the connecting client is logged. Set to 255.255.255.0 and the last octet is set to 0.

acl aclname acltype | This allows you to define Access Control Lists. This can get complicated, but it is extremely important to get right. An example of an ACL defining your internal LAN might be as follows (assuming your LAN is 192.168.7.0/24):
acl mylan src 192.168.7.0/255.255.255.0

http_access | This allows you to define who can access your cache based on the ACLs you have previously defined. An example http_access line that would allow your LAN, defined with the ACL above, to access the cache would be:
http_access allow mylan

cache_effective_user \ncache_effective_group | Set the UID the cache uses after startup. Should be set to nobody or another unprivileged user you’ve set up to run Squid.