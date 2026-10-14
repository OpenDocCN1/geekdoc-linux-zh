
The available directory options are as follows:

- **Execute CGI programs** Allows execution of CGI scripts located in this directory.
- **Follow symbolic links** The server will follow symbolic links in this directory. This correlates to the ExecCGI directive.
- **Server-side includes and execs** Server-side includes are permitted. This correlates to the FollowSymLinks directive.
- **Server-side includes** Permits server side includes, but disallows #exec command and the use of #include for CGI scripts. This correlates to the IncludesNOEXEC directive.
- **Generate directory indexes** When a URL maps to a directory in which there is no index HTML file (usually index.html, but this is a configurable option), then Apache can generate a formatted file list for the directory. This option correlates to the Indexes directive.
- **Generate Multiviews** Content-negotiated multiviews are permitted. This allows for multiple languages, character sets, and presentations to be referenced by the same URL. The client browser then negotiates with the server to select the appropriate one for the user. For more, see Content Negotiation [http://httpd.apache.org/docs/content-negotiation.html]. This option correlates to the MultiViews directive.
- **Follow symbolic links if owners match** Apache will only follow symbolic links for which the target file or directory ownership matches that of the link. This option correlates to the SymLinksIfOwnerMatch directive.

Note that if multiple items apply (inherited from a parent directory), then the ones specific to the selected directory apply, unless Merge with parent is selected. For example, if /home/httpd/penguinfoet has All permissions, but the subdirectory /home/httpd/penguinfoet/users has only ExecCGI, then that directory would only have the execute CGI option available. Merging with the parent, however, gives the subdirectory the same options, except where explicitly turned off.

## Generate MD5 digests

This option turns on generation of Content-MD5 digest headers. When enabled, Apache will generate a message digest, or fingerprint, for each static page served. When using MD5 digests, the client can be assured with a very high degree of confidence that if the content has been altered during transit from the origin server those alterations will be reflected in alterations in the message digest. The Content-MD5 standard is described in RFC 1864 [http://www.ietf.org/rfc/rfc1864.txt?number=1864] and RFC 2616 [http://www.ietf.org/rfc/rfc2616.txt?number=2616]. This option configures the ContentDigest [http://httpd.apache.org/docs/mod/core.html#contentdigest] directive. Be aware that this option can have performance implications, because the digest is generated for each request, and digests will not be created for any requests that are served by modules.

## Generate ETag header from

ETag is an HTTP response header to provide a means of differentiating two or more objects with the same URL. The header is useful for intermediary devices that perform caching, as well as client browsers that cache results. Using the ETag, an object can be uniquely identified to the client. Usually, Apache generates the ETag based on the i-node number of the file, the last modified time of the file, and the size of the file. If Select attributes is chosen, you may select any or all of these criteria. This option correlates to the FileETag [http://httpd.apache.org/docs/mod/core.html#fileetag] directive.

## Virtual server path

Very old browsers and proxies cannot address name-based virtual servers and know only how to request a site by its IP. This leads to the unfortunate effect that those browsers will only be able to reach the default website on a given IP. A workaround for this problem is to provide a path from the default server to each virtual server. Using this directive, you can define where in the path of the default server this particular virtual server will reside. So, if my virtual server www.penguinfeet.org resides on a server at IP 123.45.67.89, and an older browser visits that name, it will end up browsing to the default server on the host — which can provide the user with a list of links to virtual servers hosted on this server. If this were set to /penguinfeet, the link would then take the user to http://www.penguinfeet.org/penguinfeet/, which is the correct page! Not exactly pretty, but the web wasn't always as well thought out as it is today. And who can blame the original designers of the web for not realizing the one day everyone would have their own domain name! The good news is that those old web clients are simply no longer in use in any statistically significant quantity (they don't show up on any of my web server logs, anyway; your mileage may vary). This option configures the ServerPath [http://httpd.apache.org/docs/mod/core.html#serverpath] directive. For more on virtual hosts and the potential issues, see also the Apache Virtual Host documentation [http://httpd.apache.org/docs/vhosts/].

## Error message footer

This option allows you to add a footer to all server-generated documents (such as error pages, mod_proxy ftp directory listings, mod_info output, and so on). This is usually only needed when your Apache is acting as a proxy, as it is most useful in discovering where an error message originates from in a chain of multiple proxies. This option configures the ServerSignature [http://httpd.apache.org/docs/mod/core.html#serversignature] directive and defaults to Off.

## Automatically correct misspelled URLs?

This option configures whether Apache will attempt to correct user spelling errors in the URL. If enabled, and a URL does not match a document on the server, a check will be performed of all of the objects available that could possibly match the user's request. If one object is found that closely matches what the user requested — for example, if there was incorrect capitalizations but the object is spelled correctly or only one letter is missing — Apache will silently redirect the user to the corrected URL. If multiple possible matches are found, the user will be redirected to a page containing a list of possible pages so they may select the correct page. If no possible matches are found, the request traverses the normal error path and will result in a 404 not found error. This option correlates to the CheckSpelling [http://httpd.apache.org/docs/mod/mod_speling.html#checkspelling] directive and defaults to Off.

## Error Handling

In the event of a server error, Apache can be configured to provide custom error messages, or redirect to a local or external URL, or by default output a simple hard-coded error message. Here, you may configure any error types for which you'd like to provide a custom message. So, for example, if you wanted a custom 404 message that directed users to a local site search page (a convenient and polite thing to do), you could do that on this page. To configure the custom error responses feature of Apache, simply enter the error code, and then enter the URL or message to be displayed. See the Custom error responses documentation [http://httpd.apache.org/docs/custom-error.html] for more on this feature.

## User and Group

This page configures the user and group under which the Apache server will run. This sets the privileges the Apache and child processes will have while operating. It is strongly suggested that you set this to a user and group with as little privilege as possible (while still allowing the server to do its job). This is often configured to nobody and nogroup on many UNIX operating systems, and this is a good choice in most cases. Do not set this to root unless you know exactly what you're doing and the security implications of doing so. Note that the Apache parent process, if started as root, will remain as root, while the child processes that actually service requests will run as the user and group set here. If the parent process is started by a non-root user, Apache will not be able to su to another user, and so will run as the user that started the process. This option configures the User [http://httpd.apache.org/docs/mod/core.html#user] and Group [http://httpd.apache.org/docs/mod/core.html#group] directives.

## Aliases and Redirects

Apache provides several forms of alias and redirection. This allows you to present more unified or simpler paths to your users in the URL, as well as serve objects from outside of your server's root directory. It also allows you to redirect users to a new website during a transition period or direct their browser to the correct link if directory structure has changed.

### Document directory aliases

This allows objects to be stored in directories other than the root directory. Be aware that the aliases that end in a / will require the slash in the requested URL to be translated. This option correlates to the Alias [http://httpd.apache.org/docs/mod/mod_alias.html#alias] directive.
