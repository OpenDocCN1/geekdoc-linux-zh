# 15.4 Logging

By default, Stronghold and ApacheSSL version 3 of the SSL protocol.
 some browser/machine combinations this may cause the browsers and
possibly the OS, depending on how good its protected memory is, as well. if
you are having a problem with this, add this line to the base level (it can't be
a a VirtualHost or any other directive) of the httpd conf:

```
SSLProtocol SSLv2
```

# 15.4 Logging

As you might expect, Apache supports the Common Log Format (CLF). It
can also write its logs in the format used by NCSA's server; this is nice if
you have homegrown log analysis tools developed for NCSA.

The number of tools for analyzing http access logs is bewildering. Many
are free, but there are commercial tools out there well, though few run on
Linux. On the other hand, the free ones run on Linux than on Mac
or Microsoft (MS) Windows machines.

Which one you choose is a matter of taste. We will describe a couple
below, but you will just have to try some and see if you like them.

The log analysis tool we have found most useful is http-analyze. It is
free and information on it can be found at http://www.netstore.de/Sup-
ply/http-analyze/index.html.

One particular tool deserves special note: 3Dstats. It formats its output in
VRML which a scene viewer looks like vrweb . 3Dstats's
home page is http://www.netstore.de/Supply/3Dstats/ and Vrweb's
http://www.iicm.edu/vrweb.

If you wish to investigate other analysis tools for your httpd logs, a Web
search on http log analysis will kick up more choices than you will have time
to try out.

# 15.5 Databases and Web Servers

With the desire for dynamic content in the presentation of large amounts of
information, it is natural that databases would enter the Web equation. They
are the best and fastest way (not the most space efficient, though!) to organiza-
ize and retrieve data. There is support for many free and commercial-
bases in the popular languages used for CGI, Python, Perl, and C.
The choice of which database to use is dependent on many factors. Among
The most important is easy access via CGI or PHP if you choose to employ