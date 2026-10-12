shown here, you give the server at the other end of an FTP session the data it wants to see:

```
ftp_user squid@deepwell.com
```

You may want to use the address of your proxy firewall administrator. This will give the other FTP administrator someone to contact in case of a problem.

If you type a URL and find that the page does not exist, that page likely won't exist any time in the near future. By setting negative_ttl to a desired number of minutes, as shown in the next example, you can control how long Squid remembers that a page was not found in an earlier attempt (called negative caching):

```
negative_ttl 2 minutes
```

This isn't always a good thing. The default is five minutes, but I suggest lessening this to two or possibly one minute, if not disabling it altogether, because you want your proxy to be as transparent as possible. If users are looking for a page they know exists, you don't want the proxy to insert a delay (due to negative caching) before it actually becomes available to them.

```
cache_mgr proxy@deepwell.com
```

By setting this to your own e-mail address, you arrange to receive e-mail if Squid detects problem with cache.

```
cache_effective_user nobody
cache_effective_group nobody
```

These two lines are very important! If you are starting Squid while you are root, these two lines change the UID that Squid runs as to user nobody. This should keep any bugs in the program from changing or deleting anything.

Ultimately, a tool such as Squid should be completely transparent to your users. This removes them from the complexity of administration and allows them to browse the Web as if there were no Web proxy server. Although the details of how to do that are not presented here, you may refer to the Squid Frequently Asked Questions at http://squid.nlanr.net/Squid/FAQ/FAQ.html. Section 17 details using Squid as a transparent proxy.