# Chapter 21
## Setting Up a Web Server

# **In This Chapter**

+   - Introduction to Web servers
+   - Quick starting the Apache Web server
+   - Configuring the Apache Web server
+   - Starting and stopping the server
+   - Monitoring server activities

The World Wide Web is the fastest growing segment of the Internet, and HTTP traffic makes up over 70 percent of the total network bandwidth. Electronic commerce has provided a new virtual storefront for businesses trying to stay on the cutting edge of technology.

The Web has also been a boon to organizations seeking an inexpensive means to publish and distribute information. And with increasing computing power, decreasing prices, free operating systems such as Linux, and free Web servers such as Apache and TUX, it’s getting even easier for anyone to establish a presence on the Web.

This chapter shows you how to install and configure the Apache Web server. Each of the server’s configuration files is described and explained in detail. You learn about various options for starting and stopping the server, as well as how to monitor the activity of a Web server. Security is an issue addressed throughout the chapter in the descriptions and examples.

> **NOTE:** The current version of Red Hat Linux comes with Apache version 2.0. Apache 2.0 includes support for a new Apache application programming interface, UNIX threading (for multi-processing), Internet Protocol version 6, and multiple protocols. A handful of new modules have also been added. With 2.0, the package names apache and apache-manual changed to httpd and httpd-manual.

# ### Introduction to Web Servers

The World Wide Web, as it is known today, began as a project of Tim Berners-Lee at the European Center for Particle Physics (CERN). The original goal was to provide one consistent interface for geographically dispersed researchers and scientists who needed access to information in a variety of formats. From this idea came the concept of using one client (the