
![](img/d84604054810a13cacfdac212ebee2f7_110_0.png)

## SERVER AND DAEMON CONFIGURATION

Clicking the Servers tab on the Webmin category bar brings you to what is probably the most interesting of the Webmin pages. It is here that all of the various complex servers and daemons can be configured. Webmin provides standard modules for a large number of the most popular servers and daemons in use on network systems in the world today, and more are being written all the time.

### Introduction to Servers

The Servers Webmin category allows for administration of the server applications that run on a system, which provide some service to clients on the network. One example is the Apache web server daemon. Clicking on the Apache icon in this category allows you to edit the Apache configuration files, which are usually located in /etc/httpd/ conf. Most modules located in Servers will enable you to edit some configuration file found in /etc or some subdirectory therein. One of the most impressive features of Webmin is the ability to allow you to edit files without damaging existing hand-edited configuration details.

![](img/d84604054810a13cacfdac212ebee2f7_111_0.png)

Figure 6-1: Servers category

The root of much of Webmin’s popularity is the ability for an administrator to perform some tasks through the Webmin interface without being forced to do all tasks with Webmin. Unlike some graphical front ends for UNIX systems, Webmin leaves an edited file intact as much as is possible. Comments are untouched, and the ordering of directives is not changed. This results in a system that can be configured through Webmin and through hand-editing of configuration files, but with no conflict between the two methods.

A side effect of this feature is that Webmin generally must provide a one-to-one interface to configuration files in order to ensure that configuration options are not confused and to ensure that a savvy administrator gets what is expected from the Webmin output. This means that Webmin is not an “easier” way to administer a UNIX system. The administrator still must understand the tools he or she is administering with Webmin. For example, configuring DNS from Webmin requires an understanding of named and its required configuration files. The same applies to squid, httpd, sendmail, and so on. Webmin can make the learning process somewhat quicker, however, as all of the options are present on the display, which may or may not be the case with configuration files.

![](img/d84604054810a13cacfdac212ebee2f7_112_0.png)

## APACHE WEBSERVER

The Apache module is broken up into several sections to address different aspects of an Apache configuration. On the main page, these sections are grouped into Global Configuration and Virtual Servers groups. Using virtual servers it is possible to locate several websites with unique domain names on a single IP address, in order to conserve the rapidly diminishing IPv4 address space.

In the context of the Apache module, Global Configuration refers to configuration information that will apply to all virtual hosts that are run from the same httpd daemon. It is usually unnecessary to run more than one httpd daemon on a single machine but it is possible. It is also possible to manage more than one such daemon with Webmin via the module cloning feature.

> NOTE The official Apache documentation [http://httpd.apache.org/docs/] is a good source of additional information about Apache and its modules.

### Global Configuration

Global Configuration is found on the top half of the divided Apache module page, as shown in Figure 7-1. It provides access to the various options that will be shared across all virtual servers, such as which modules to load, network addresses, MIME types, etc. The options configured here will apply to every virtual server and the default server. To configure an option for one specific virtual server it must be configured in the Virtual Servers Configuration section.

![](img/d84604054810a13cacfdac212ebee2f7_113_0.png)

Figure 7-1: Apache Global Configuration

### Processes and Limits

This page provides the following options, which set many of the limits for Apache. Generally, the defaults are reasonable, but may need to be altered for high load or low memory situations. The options on this page cover two distinct but related limits that are configurable in Apache.

The first set of limits is related to the length or number of request headers that will be accepted by the server. A request header is a term that refers to all of the information that a client sends to the server to indicate the object it would like to receive. The most important portion of the request header is usually made up of the HTTP method (such as GET, POST, HEAD, and so on), the URI (the complete path and domain name of the object being referred to), and the HTTP protocol version number.

The second set of limits refers to connection and process specific limits of Apache. Apache usually operates in what is known as a process-per-connection mode, wherein each client connection to the server will be served by a single and independent httpd process. Thus to provide service to 30 simultaneous clients, the system will run 30 Apache processes.

### Maximum headers in request

Sets the maximum number of request headers accepted per request. Each time a web client (usually a web browser) makes a connection to a web server, it includes request headers to indicate information about the encoding capabilities, HTTP version support, cache-control, content negotiation and other information about the client agent. As HTTP standards and non-standard extensions to the HTTP protocol have been developed, the number of request headers usually received has risen slowly, but is rarely more than 20. The LimitRequestFields [http://www.apache.org/docs/mod/core.html#limitrequestfields] directive in the Apache configuration file is modified by this option and usually defaults to 100.

It may be possible to prevent certain types of denial-of-service attacks by restricting the number of headers accepted, though it is unlikely to be a problem at the default value. It should rarely need to be altered from its default, unless clients receive error messages from the server indicating too many headers were in the request.

### Maximum request header size

Defines the maximum header field size that will be permitted. Apache sets aside a buffer for processing of header entries received from the client. This buffer must be large enough to contain a single header entry in its entirety. The LimitRequestFieldSize [http://www.apache.org/docs/mod/core.html#limitrequestfieldsize] directive is modified by this option, and it usually defaults to 8190 and this value is also the normal maximum value possible. It is worth noting that the maximum value for this option is system dependent and is compiled into the Apache executable when it is built. Raising this value above the default of 8190 may not be supported on your Apache and should not be necessary under any normal circumstances.

### Maximum request line size

Defines the maximum length of an HTTP request line. The request line contains the HTTP method, the complete URL, and the protocol version. The accepted line size needs to be long enough to contain any resource name on the system, and the default is generally recommended. This option edits the LimitRequestLine [http://www.apache.org/docs/mod/core.html#limitrequestline] directive in the Apache configuration and defaults to 8190 bytes, which is also the compiled-in upper bound for this value.

This option rarely needs to be altered from its default, but may be useful in preventing certain types of denial-of-service attacks by preventing client applications from overloading the server with many extremely large and complex request lines.

### Maximum concurrent requests

The maximum number of allowed concurrent requests. Each request to Apache spawns a new daemon, and this defines the upper limit on how many such daemons will be spawned to answer requests. This option correlates to the
