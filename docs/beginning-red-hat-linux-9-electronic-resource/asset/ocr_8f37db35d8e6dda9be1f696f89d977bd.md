The server name you specify should be a FQDN (because it will need to be resolved to an IP address by DNS). If you haven't setup a DNS, then you can enter the IP address allocated to the Linux server instead, like this:

```
ServerName 192.168.0.99
```

+   4.  Save the `httpd.conf` file, and close it.

+   5.  Restart the `httpd` daemon to reflect the changes. To do this, use Red Hat Services Configuration GUI, or the `httpd` command line script as described earlier in this chapter:

```
# service httpd restart
Stopping httpd:					[  OK  ]
Starting httpd:					[  OK  ]
```

Now browse to http://localhost again, to check that the web server is still serving web pages. You should see the Apache Test Page that we saw earlier in this section.

There are many configuration settings that you can control via the `httpd.conf` configuration file. For more information, refer to the Apache web server documentation at http://httpd.apache.org/docs-2.0/.

# Setting up Your First Web Site

In the remainder of this section, we'll set up a simple web site, which will be accessible on the network. This will involve creating a simple HTML web page, and saving it to a location on the hard disk that is used by the web server to store published web pages. Then, when a user requests the page, the web server will be able to respond by retrieving it from this location and sending it to the requesstor.

# Try It Out	Publishing Your First Web Page

+   1.  Launch an editor (you can use a dedicated web page editor such as Mozilla Composer if you have it installed; alternatively, `gedit` will do). Create a new file – call it `index.html` and save it in the directory `/var/www/html`.

+   2.  Type some HTML into the file. For example:

```
<html>
<head>
<title>Beginning Red Hat Linux - Apache Test Page</title>
</head>
<body>
<center>
<h1>Beginning Red Hat Linux - Apache Test Page</h1>
This is the first page of your web site!
```