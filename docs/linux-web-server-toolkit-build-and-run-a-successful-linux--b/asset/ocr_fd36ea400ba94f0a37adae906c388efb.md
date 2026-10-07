# Linux Web Server Toolkit

In your log file entries, you can have either an IP address or a domain name (a hostname) recorded as the place where the request came. The difference is between your log entry looking like this (note the first item in the entry):

```
dynamo.target.org - [02/Sep/1997:14:02:22 -0800] GET
/Index.html HTTP/1.0 200 44398
```

Or this:

```
204.98.13.15 - [02/Sep/1997:14:02:22 -0800] GET
/Index.html HTTP/1.0 200 44398
```

Obviously, the first one is more useful in determining who is really accessing your Web site. You can tell in a glance (with the help of a few simple statistics programs) which types of sites from which countries are accessing your Web site. You can see if someone from a competitor has been spending a lot of time browsing your site.

Of course, you want DNS names recorded. However, looking up hostnames for requests that only come with IP addresses takes a lot of extra time that your Web server could be using to service the next request. High-end statistics programs would up DNS names anyway, and do more job of it during the process of preparing reports about your site. If you have those, or if you want your site's energy more fully dedicated to servicing browser requests, choose the options to record IP addresses instead of DNS names.

You can choose the log accesses using the Common Logfile Format, which I've mentioned in several places, or you can select exactly what you want to have logged among all the information available to the Web server for each request. Remember, however, that not all browsers submit all the fields you may be logging – there may be some holes in the data. If you choose not to use the Common Logfile Format, just check the boxes for the fields that you wanted in your log files. I recommend using the Format String in the log file (check that at the bottom of the page) so that statistics programs can interpret the data.

Finally, you can enter a list of computers, either as hostnames or IP addresses, that should not be logged. This is mostly used for keeping references to your own sites out of the log. For example, if you use a few systems to create and check your HTML files, those systems would be listed in your log log. But such systems not really count as customer visitors to your site. This field allows you to avoid logging this type of hit, so you don't have to bother with removing some statistical information later on.

# Generate Report

The Generate Report page allows you to generate a simple statistical report from the log files I discussed in the Server Status section.

Basically, there are three types of statistics that are generated for this simple report. You can specify something about how these statistics are organized in the page, then choose OK to create the report in the filename that you provide in the