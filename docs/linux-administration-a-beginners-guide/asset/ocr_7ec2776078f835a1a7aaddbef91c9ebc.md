```
1 IN NS ns.domain.com.
2 IN PTR img.domain.com.
3 IN PTR mail.domain.com
4 IN PTR technics.domain.com
5 IN NS ns.domain.com
6 IN PTR peanutbutter.com
```

We don't have to create any files to be secondary for example.com. We only need to add the entries we already have in the /etc/named.conf file.

And that's it: a complete configuration for a primary domain.

# # THE DNS TOOLBOX

This section describes a few tools that you'll want to get acquainted with as you work with DNS. They'll help you to troubleshoot problems more quickly.

# ## nslookup

The **nslookup** tool is really the master of all DNS tools. By learning all of the features nslookup has to offer, you can eliminate the need to learn several of the smaller tools that come with BIND.

In it's simplest use, nslookup allows you to resolve host names into IP addresses from the command line. For example:

```
[root@ford root]# nslookup theorw.com
Server: localhost
Address: 127.0.0.1

Name: theorw.com
Address: 209.133.83.16
```

In the output, we see the name of the server that nslookup queried by default, and then the answer returned by that server. This example was run on a name server, so it was configured to look back at itself to resolve host names; thus, the server name is localhost.

We can also use nslookup to perform reverse lookups. For example:

```
[root@ford root]# nslookup 209.133.83.16
Server: localhost
Address: 127.0.0.1

Name: taz.hyperreal.org
Address: 209.133.83.16
```

This can lead to all kinds of interesting discoveries. In this case, we see that theorw.com is the same as taz.hyperreal.org. It's likely that taz.hyperreal.org is also "virtual hosting" other domains, as well.