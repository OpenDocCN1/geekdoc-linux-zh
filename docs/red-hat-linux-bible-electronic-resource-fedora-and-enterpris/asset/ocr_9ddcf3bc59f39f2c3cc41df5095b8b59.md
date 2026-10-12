+   * The cached files would exist in `/var/cache/mod_proxy`.
+   * Cache size is limited to 500 Kbytes.

You may want to allow a much larger `CacheSize`, and possibly set a short `CacheGCInterval`, but otherwise the supplied values are reasonable. The `CacheGCInterval` value can be a floating-point number (for example, 1.25 indicates 75 minutes).

# ## Configuring virtual hosting

If you have one Web server computer, but more than one domain that you want to serve with that computer, you can set up Apache to do virtual hosting. With virtual hosting, a single IP address can be the access point for multiple domain names.

With virtual hosting, when a request comes into your Apache server from a Web browser through a particular IP address on your computer, Apache checks the domain name being requested and displays the content associated with that domain name. As an administrator of a Web server that supports virtual hosting, you must make sure that everything that needs to be configured for that virtual server is set up properly (you must define such things as locations for the Web content, log files, administrative contact, and so on).

Virtual hosting is defined with the `VirtualHost` tags. Information related to virtual hosts in the `/etc/httpd/conf/httpd.conf` file is shown in the following code:

```
```
### Section 3: Virtual Hosts
#
# VirtualHost: If you want to maintain multiple domains/hostnames on
# your machine you can setup VirtualHost containers for them. Most
# configurations use only name-based virtual hosts so the server
# doesn't need to worry about IP addresses. This is indicated by the
# asterisks in the directives below.
#
# Please see the documentation at
# <URL:http://httpd.apache.org/docs-2.0/vhosts/>
# for further details before you try to setup virtual hosts.
#
# You may use the command line option '-S' to verify your virtual host
# configuration.
#
# Use name-based virtual hosting.
#
#NameVirtualHost *
#
# VirtualHost example:
# Almost any Apache directive may go into a VirtualHost container.
# The first VirtualHost section is used for requests without a known
# server name.
```
```