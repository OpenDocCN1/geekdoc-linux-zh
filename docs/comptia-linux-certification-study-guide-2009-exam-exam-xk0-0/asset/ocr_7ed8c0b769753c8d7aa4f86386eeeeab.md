curl http://www.shell.com

The first couple of lines of the output are shown below (highly truncated)

```
```
$ curl www.shell.com
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
  xml:lang="en" lang="en">
<head>
```
```

# **Apache (HTTP) and Tomcat**

There are many different Web (HTTP) servers available for Linux, but the most common by far is the Apache Web server developed and maintained by the Apache Software Foundation, whose main Web page is located at www.apache.org/. The Apache Web server is probably the most popular Web server on the Internet today. While we will only look at the HTTP server, the foundation also has a large number of other projects that are continually being worked on, all of which are described on their home page.

The Apache HTTP server is an open-source server that has been developed for a number of operating systems including Linux, UNIX, and Microsoft Windows. While the server code is usually included with a Linux distribution, this will typically be out of date to some extent. If the server is going to be used to serve pages to the Internet, the latest version should always be downloaded from the http://apache.org Web site, which will include all the latest security fixes. The installation of Apache will be to /usr/local/apache2 as a default, but this can be configured by the user at install time. The installation will take up about 50 MB of disk space, which will include a number of options. Any user pages will increase the amount of disk space needed. The method of installation will be similar for other packages: download, extract, configure the makefile, compile, install, and make any additional configuration changes. The following sections will look at how you can configure the server to suit your specific needs.

# *Apache Configuration*