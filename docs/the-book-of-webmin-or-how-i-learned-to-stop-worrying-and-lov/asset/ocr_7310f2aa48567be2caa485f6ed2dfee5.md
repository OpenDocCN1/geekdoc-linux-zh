write modules to improve the features of Squid (Figure 12-9). That being said, some of Squid’s standard functionality is also provided by helper programs. The standard helper programs include dnsserver, pinger, and several authentication modules. Third-party modules include redirectors, ad blockers, and additional authentication modules.

> NOTE
> Squid versions from 2.3 onward do not use the dnsserver helper program by default, replacing it with an internal non-blocking DNS resolver. This new internal DNS resolver is more memory and processor efficient, so is preferred. But in some circumstances, the older helper program is the better choice. If your Squid must be able to resolve based on any source other than a DNS server, such as via a hosts file or NIS, then you may need to use the external dnsserver helper.

![](bbox=[0.25, 0.38, 0.78, 0.58])

Figure 12-9: Cache helper program

# FTP column width

The column width for auto-generated web pages of FTP sites queried through Squid when Squid is in forward proxy mode. Squid provides limited FTP proxy features to allow browsers (even older, non-FTP aware browsers) to communicate with FTP servers. This option gives some control over how Squid formats the resulting file lists. This option correlates to the ftp_list_width and defaults to 32.

> NOTE
> Squid only provides FTP proxy and caching services when acting as a traditional proxy, not when acting transparently. Squid does not currently provide FTP caching or proxying for standard FTP clients. The clients must be HTTP clients, for which Squid can provide gateway services.

# Anon FTP login

The email address Squid uses to log in to remote FTP servers anonymously. This can simply be a username followed by an @ symbol, which your domain name can be automatically attached to. Or it can be a full email address. This should be something reasonable for your domain, such as wwwuser@mydomain.com, or in the domainless case first mentioned, Squid@, which happens to be the default for this option. This corresponds to the ftp_user directive.