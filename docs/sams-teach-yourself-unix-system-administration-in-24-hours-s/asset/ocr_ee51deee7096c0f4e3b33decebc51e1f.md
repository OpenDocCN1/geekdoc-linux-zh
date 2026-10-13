In this hour, you'll learn how to

+   - Set up your Web server
+   - Configure Apache with the httpd.conf file
+   - Test connectivity and capabilities

# Setting Up Your Web Server

The first step in this journey is to see what version of Apache you might have included with your Unix OS. As of this writing, Red Hat Linux ships with Apache 1.3.20, Mac OS X includes Apache 1.3.23, and Solaris includes Apache 1.3.12 (in the somewhat odd location of /usr/apache/).

![](bbox=[0.25, 0.53, 0.3, 0.62])

> To identify your version, find the httpd binary (use locate) and use the -v flag. For example: /usr/sbin/httpd -v.

The Apache 2.0 release is available through the Apache Web site (www.apache.org), and it's pretty stable, but you might want to stick with your current distribution of Apache if you're just serving up HTML- and CGI-based pages. What's important is that you at least have 1.3. If you have 1.2, or earlier, it's time to upgrade: Major architectural and performance changes were introduced with 1.3, most notably the inclusion of how the configuration files are laid out.

# Task 23.1: Bringing Apache to Life

Before we start, a quick note: If you're wondering why we're focused on Apache versus one of the other possible servers (notably Netscape), the answer is contained in this brief quote from the Apache Web site:

> Apache has been the most popular Web server on the Internet since April of 1996. The March 2002 Netcraft Web Server Survey (http://netcraft.com/survey/) found that 54% of the Web sites on the Internet are using Apache, thus making it more widely used than all other Web servers combined.

+   1. The first and most logical test is this: Is the Web server running on your system or not? There are a couple of ways to test that, including the obvious ps -aux|grep httpd, but I prefer to try and connect directly to the server and see what happens:

```
# telnet localhost http < /dev/null
Trying 127.0.0.1...
telnet: connect to address 127.0.0.1: Connection refused
```