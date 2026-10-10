# **Chapter 20**

# **Setting Up a Web Server**

# **In This Chapter**

+   • Introducing Web servers
+   • Quick starting the Apache Web server
+   • Configuring the Apache Web server
+   • Starting and stopping the server
+   • Monitoring server activities

Approximately 46 percent of all Web sites today are powered by the open source Apache Web Server Project (compared with about 22 percent for Microsoft Web servers). In October 2009, Netcraft (`http://www.netcraft.com`) reported receiving responses from more than 231 million sites, more than 105 million of which were running Apache. As registration of Internet domain names continues to grow at an average rate of more than six million a month, Apache is getting the lion’s share of new Web sites being launched.

The Web has also been a boon to organizations seeking an inexpensive means to publish and distribute information. Using the Fedora distribution that comes with this book, you can launch your own Web site using software available from the Apache project. Combine your own domain name, Internet connection, and Fedora to create your own presence on the World Wide Web.

This chapter shows you how to install and configure the Apache Web server. Each of the server’s configuration files is described and explained in detail. You learn about various options for starting and stopping the server, as well as how to monitor the activity of a Web server. Related security concerns and practices are addressed throughout the chapter in the descriptions and examples, as well as in a special Web server security section (“Protecting Web Servers with Certificates and Encryption”) in Chapter 13.

> **NOTE:** The current version of Fedora comes with Apache version 2.2.13. Patche 2.2.13 includes support for a new Apache API, UNIX threading (for multiprocessing), Internet Protocol version 6 (IPv6), and multiple protocols. If you have been using a pre-2.0 version of Apache, note that the package names `apache` and `apache-manual` have changed to `httpd` and `httpd-manual`, respectively.