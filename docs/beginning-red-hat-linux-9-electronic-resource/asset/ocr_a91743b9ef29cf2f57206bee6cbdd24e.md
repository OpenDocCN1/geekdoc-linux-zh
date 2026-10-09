As we've said, your network topology, and the network configuration of your machine(s), may be different; but many of the principles in this chapter remain the same, and you should be able to get any of these services going regardless of your own environment.

We will assume that you have root access to the Red Hat Linux server. Throughout the chapter, we'll use the terms *Linux server* and *client* to refer to the Red Hat Linux 9 server machine and the Microsoft Windows 2000 client machine respectively.

# Setting up a Web Server

When we want to publish web pages on the Internet (or on an intranet), we use a web server. In essence, a **web server** is an application that does two things:

+   - It listens for page requests.
+   - When it receives a page request, it examines the request and responds with the page that was requested.

For example, when you use a web browser to browse http://www.wrox.com, the browser turns this into a **request** message and sends it across the Internet to Wrox's own web server. When the web server receives this request, it processes it, works out what page you requested, puts that page together from whatever resources are necessary, and sends the page back to your browser, in the form of a **response** message.

Of course, there are many different web browsers in existence (including Mozilla, Opera, Internet Explorer, and others), and there are also a great many types of web server software. To enable a browser to request pages from a web server, they communicate using **Hypertext Transfer Protocol (HTTP)** – this is the standard protocol for the Internet. The request and response messages are composed using HTTP, and this is what allows *any* browser to request web pages from *any type* of web server.

> By default, all web servers listen for HTTP requests on port 80. Web servers also use port 443 to listen for requests made through secure HTTP connections, over SSL (secure sockets layer), through a protocol called HTTPS.

So, if you want to publish your own web site, you'll need a machine with some web server software. However, the chances are that if you build your own web site, you probably won't want to expose it to the Internet from your *own* machine. There are security and maintenance issues to manage, and you'd need to buy enough hardware and bandwidth to handle all the page requests. More likely, you'd choose an Internet service provider (ISP), and use their web servers to host your web site for you.

So, why would you want to install a web server on your Red Hat Linux machine? Well, here are two scenarios: