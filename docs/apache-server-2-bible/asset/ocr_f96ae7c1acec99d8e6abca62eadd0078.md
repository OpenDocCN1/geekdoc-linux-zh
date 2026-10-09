When a request is received for http://www.mydomain.com/download/any path from a host called dialup001.demon.uk, the request needs to be redirected to the Web site www.mydomain.uk/download/; similarly, any requests from hosts that belong to the top-level domains .com, .net, .edu, and .org are routed to the www.mycompany.com/download/ site.

Here are the rules that are needed for the above setup:

```
RewriteMap     sitemap       txt:path/to/site-redirect.map
RewriteRule     ^/download/(.*)  % {REMOTE_HOST}:$1   [C]
RewriteRule     ^\.\+ ([. -z-A -z])+: (::)\* % {site map: $1} www.mydomain.com/download/$2 [R,L]
```

Figure 9-7 illustrates the use of this rule.

![](bbox=[0.18, 0.41, 0.81, 0.79])

As Figure 9-7 shows, when a host such as dialup001.demon.uk requests the www.mydomain.com/download/index.html page (1), the first rule rewrites the request by using the hostname of the requesting host as follows:

```
dialup001.demon.uk::index.html
```

Then the next rule in the chain is applied. This rule gets applied when the search pattern matches and the substitution URL is created by looking up the map file for the top-level domain. If no matches are found, the default www.mydomain.com is