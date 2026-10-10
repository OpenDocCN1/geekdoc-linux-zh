to Firefox and enter a new URL, you should see the Squid error page informing you that you do not have access to the requested site.

The reason you are now blocked from the proxy is because Squid reads its ACL lines in sequence, from top to bottom. If it finds a line that conclusively allows or denies a request, it stops reading and takes the appropriate action. So, in the previous lines, localhost is being denied in the first line and allowed in the second. When Squid sees localhost asking for a site, it reads the deny line first and immediately sends the error page— it does not even get to the allow line. Having a deny all line at the bottom is highly recommended so that only those you explicitly allow are able to use the proxy.

Go back to editing the configuration file and remove the deny localhost and allow localhost lines. This leaves only deny all, which blocks everyone (including the localhost) from accessing the proxy. Now we are going to add some conditional allow statements: We want to allow localhost only if it fits certain criteria.

Defining access criteria to done with the acl lines, so above the deny all line, add this:

```
acl newssites dstdomain news.bbc.co.uk slashdot.org
http_access allow newssites
```

The first line defines an access category called newssites, which contains a list of domains (dstdomain). The domains are news.bbc.co.uk and slashdot.org, so the full line reads, “create a new access category called newssites, which should filter on domain, and contain the two domains listed.” It does not say whether access should be granted or denied to that category; that comes in the next line. The line http_access allow newssites means, “allow access to the category newssites with no further restrictions.” It is not limited to localhost, which means this applies to every computer connecting to the proxy server.

Save the configuration file and rerun the kill -SIGHUP line from before to restart Squid; then go back to Firefox and try loading http://fedora.redhat.com. You should see the same error as before because that was not in the newssites category. Now try http://news.bbc.co.uk, and it should work. However, if you try http://www.slashdot.org, it will not work, and you might also have noticed that the images did not appear on the BBC News website either. The problem here is that specifying slashdot.org as the website is very specific: It means that http://slashdot.org will work, whereas http://www.slashdot.org will not. The BBC News site stores its images on the site http://newsimg.bbc.co.uk, which is why they do not appear.

Go back to the configuration file, and edit the newssites ACL to this:

```
acl newssites dstdomain .bbc.co.uk .slashdot.org
```

Putting the period in front of the domains (and in the BBC’s case, taking the news off also) means that Squid allows any subdomain of the site to work, which is usually what you will want. If you want even more vagueness, you can just specify .com to match *.com addresses.