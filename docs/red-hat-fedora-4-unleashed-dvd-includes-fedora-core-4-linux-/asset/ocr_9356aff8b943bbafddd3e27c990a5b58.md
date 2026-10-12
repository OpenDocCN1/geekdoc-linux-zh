# Configuring Apache for Peak Performance

Use the options in the Performance Tuning tab to configure Apache to provide peak performance in your system. Options in this tab set the maximum number of connections, connection timeouts, and number of requests per connection. When setting this number, keep in mind that, for each connection to your server, another instance of the HTTPD program might be run, depending on how Apache is built. Each instance takes resources such as CPU time and memory. You can also configure details about each connection such as how long, in seconds, before a connection times out and how many requests each connection can make to the server.

# Other Web Servers for Use with Fedora

Of course, other web servers can be used with Fedora. Apache is by far the most popular, but this does not rule out the others.

To determine the best web server for your use, consider the needs of the website you manage. Does it need heavy security (for e-commerce), multimedia (music, video, and pictures), or the capability to download files easily? How much are you willing to spend for the software? Do you need software that is easy to maintain and troubleshoot or that includes tech support? The answers to these questions might steer you to something other than Apache.

The following sections list some of the more popular alternatives to using Apache as your web server.

# thttpd

It is not entirely clear what the t in thttpd stands for. Meanings alternate between *tiny*, *turbo*, and *throttl*ing, depending on whom you ask. Whatever meaning you opt for, it is clear that thttpd is *not* big and slow.

*Throttl*ing, in the context of thttpd, is a process in which incoming URL calls are kept under control for a certain page or collection of pages on the website. If traffic to these pages hits a defined limit, the requesters for the page are sent a try again code until the traffic returns to a more manageable level.

thttpd is, on the surface, a simple little HTTP server that can handle a fair amount of traffic with minimal strain. Although not as robust as Apache, it does feature a throttling control—something that is not readily available for Apache.

thttpd is available as freeware from the thttpd website (http://www.acme.com/software/thttpd).

# Sun ONE Web Server

Despite the Netcraft numbers shown previously in Table 19.1, there is evidence that the Sun Java System Web Server (formally known as the iPlanet Web Server, and subsequently Sun ONE Web Server) might be even more popular than Apache in strictly corporate