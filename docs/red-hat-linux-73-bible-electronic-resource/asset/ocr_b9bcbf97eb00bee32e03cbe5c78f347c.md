# **Chapter 21**

# # Setting up a Web Server

# **In This Chapter**

+   - Introduction to Web servers
+   - Quick starting the Apache Web server
+   - Configuring the Apache Web server
+   - Starting and stopping the server
+   - Monitoring server activities

The World Wide Web is the fastest growing segment of the Internet, and HTTP traffic makes up over 70 percent of the total network bandwidth. Electronic commerce has provided a new virtual storefront for businesses trying to stay on the cutting edge of technology.

The Web has also been a boon to organizations seeking an inexpensive means to publish and distribute information. And with increasing computing power, decreasing prices, free operating systems such as Linux, and free Web servers such as Apache and TUX, it’s getting even easier for anyone to establish a presence on the Web.

This chapter shows you how to install and configure the Apache Web server. Each of the server’s configuration files is described and explained in detail. You learn about various options for starting and stopping the server, as well as how to monitor the activity of a running Web server. Security is an issue addressed throughout the chapter in the descriptions and examples.

> **NOTE:** Red Hat Linux 7.3 comes with Apache version 1.3-23. An Apache 2.0 version has recently become available. The new version includes support for a new Apache application programming interface, UNIX threading (for multi-processing), Internet Protocol version 6, and multiple protocols. A handful of new modules have also been added. Visit the Apache web site (`www.apache.org`) for details on Apache 2.0.

# ## Introduction to Web Servers

The World Wide Web, as it is known today, began as a project of Tim Berners-Lee at the European Center for Particle Physics (CERN). The original goal was to provide one consistent