
![](img/774d40fd20903495c5cd00e2efad3f33_584_0.png)

FIGURE 19.3 system-config-httpd's Virtual Host Properties dialog box gives you access to numerous options for configuring the properties of an Apache virtual host.

## Configuring the Server

The Server tab, shown in Figure 19.4, enables you to configure things such as where the lock file and the PID file are kept.

In both cases, you should use the defaults. You can also configure the directory where any potential core dumps will be placed.

Finally, you can set which user and group Apache is to run as. As mentioned in a previous note, for security reasons, you should run Apache as the user named apache and as a member of the group apache.

![](img/774d40fd20903495c5cd00e2efad3f33_584_1.png)

FIGURE 19.4 system-config-httpd's Server configuration tab.

## Configuring Apache for Peak Performance

Use the options in the Performance Tuning tab to configure Apache to provide peak performance in your system. Options in this tab set the maximum number of connections, connection timeouts, and number of requests per connection. When setting this number, keep in mind that, for each connection to your server, another instance of the HTTPD program might be run, depending on how Apache is built. Each instance takes resources such as CPU time and memory. You can also configure details about each connection such as how long, in seconds, before a connection times out and how many requests each connection can make to the server.

## Other Web Servers for Use with Fedora

Of course, other web servers can be used with Fedora. Apache is by far the most popular, but this does not rule out the others.

To determine the best web server for your use, consider the needs of the website you manage. Does it need heavy security (for e-commerce), multimedia (music, video, and pictures), or the capability to download files easily? How much are you willing to spend for the software? Do you need software that is easy to maintain and troubleshoot or that includes tech support? The answers to these questions might steer you to something other than Apache.

The following sections list some of the more popular alternatives to using Apache as your web server.

### thttpd

It is not entirely clear what the t in thttpd stands for. Meanings alternate between *tiny*, *turbo*, and *throttl*ing, depending on whom you ask. Whatever meaning you opt for, it is clear that thttpd is *not* big and slow.

*Throttl*ing, in the context of thttpd, is a process in which incoming URL calls are kept under control for a certain page or collection of pages on the website. If traffic to these pages hits a defined limit, the requesters for the page are sent a try again code until the traffic returns to a more manageable level.

thttpd is, on the surface, a simple little HTTP server that can handle a fair amount of traffic with minimal strain. Although not as robust as Apache, it does feature a throttling control—something that is not readily available for Apache.

thttpd is available as freeware from the thttpd website (http://www.acme.com/software/thttpd).

### Sun ONE Web Server

Despite the Netcraft numbers shown previously in Table 19.1, there is evidence that the Sun Java System Web Server (formally known as the iPlanet Web Server, and subsequently Sun ONE Web Server) might be even more popular than Apache in strictly corporate arenas. Netcraft has rated Sun Java System Web Server number one in market share among Fortune 100 websites.

The server got its start as the Netscape Enterprise Server—one of the first powerful web servers ever to hit the market. Sun ONE Web Server comes in many flavors, and all of them are big. In addition to the enterprise-level web server that can be run on Red Hat, the software features application, messaging, calendar, and directory servers—just to name a few.

Sun ONE Web Server is great for handling big web needs, and it comes with an appropriately big price tag: $1,495 (U.S.) per CPU. It's definitely not something to run the school website—unless your school happens to be a major state university with several regional campuses. For more information on Sun Java System Web Server, you can visit its website (http://wwws.sun.com/software/products/web_srvr/home\_web\_srvr.html).

### Stronghold

If you're looking for something a little more secure than Apache but still don't want to lose the Apache functionality, you can purchase Stronghold from Red Hat Software.

Although not a web server as such, Stronghold is a server add-on that provides 128-bit cryptography and security certificates to the Apache web server (which is included in your purchase of Stronghold).

Stronghold supports SSL and TLS security standards, as well as many of the certificate standards on the market today.

The price for this kind of security is not particularly cheap. The software, which can be previewed at http://www.redhat.com/software/stronghold/, was advertised in 2004 at $995 (U.S.) per year.

### Zope

Zope is another open-source web server. Although it is still relatively young and might not have as much flexibility as Apache, it is making strong inroads in the web server market.

What makes Zope different from Apache is the fact that it is managed through a completely web-based graphic interface. This has broad appeal for those who are not enthused about a command-line-only interface.

Zope is a product of the Zope Corporation (formerly Digital Creations), the same firm that made the Python programming language. And, like all things open source, it is free. Information on Zope can be found at both http://www.zope.com (for the commercial version) and http://www.zope.org (for the open-source version).

### Zeus Web Server

Fedora sites can also use the Zeus Web Server from Zeus Technology. This server offers a scalable SSL implementation, security settings across multiple websites, and an online administration server. The current price is $1,700 for a host platform with up to two CPUs, but load balancing via the Zeus Load Balancer costs $12,000 for each pair of load-balancing computers.

You can get more information about the Zeus Web Server at http://www.zeus.com/ products/zws/.

### TWiki

TWiki is a web-based collaboration tool. In use, it provides pages that resemble a regular website, but logged-in users can add content or make other modifications using a web browser. Content is generated while maintaining a log of all changes. TWiki is a collection of Perl scripts that can extend and complement Apache's capabilities. TWiki is available at no cost under the GPL from http://www.TWiki.org. You learn more about this tool in “Collaborating with TWiki,” in Chapter 8, “On the Internet: Surfing the Web, Writing Email, and Reading the News.”

![](img/774d40fd20903495c5cd00e2efad3f33_587_0.png)

You will use these commands when managing your Apache web Server in Fedora:

- `apacheectl`—Server control shell script included with Apache
- `system-config-httpd`—Red Hat’s graphical web server configuration tool
- `httpd`—The Apache web server
- `konqueror`—KDE’s graphical web browser
- `elinks`—A text-based, graphical menu web browser
- `firefox`—The premier open-source web browser

## Reference

There’s a plethora of Apache documentation online. For more information about Apache and the subjects discussed in this chapter, look at some of the following resources:

- http://news.netcraft.com/archives/web_server_survey.html—A statistical graph of web server usage by 53,341,867 servers (as of August 2004). The research points out that Apache is by far the most widely used server for Internet sites.
- http://www.apache.org/—Extensive documentation and information about Apache are available at The Apache Project website.
- http://www.apacheweek.com/—You can obtain breaking news about Apache and great technical articles at The Apache Week site.
- http://apachetoday.com/—Another good Apache site. Original content as well as links to Apache-related stories on other sites can be found at Apache Today’s site.
- http://www.hwg.org/—HTML, CGI, and related subjects are available at The HTML Writers Guild site.
