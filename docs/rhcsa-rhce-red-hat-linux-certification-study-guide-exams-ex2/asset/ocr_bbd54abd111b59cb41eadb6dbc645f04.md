+   6. Add an appropriate index.html file to the /var/www/html/chapter directory. It's okay to use a text editor to enter a simple line such as "test was successful." No HTML coding is required.
+   
+   7. Create the /etc/httpd/testpass file with an appropriate password. On my system, I created a web password for user michael in the noted file with the following command:
+   Additional users can be added without the -c switch.
+   
+   8. Test the result, preferably from another system. (In other words, make sure the firewall allows access from at least one remote system.)
+   
+   9. You should now see a request for a username and password, with the comment associated with the AuthName directive. Enter the username and password just added to /etc/httpd/testpass and observe the result.
+   
+   10. Close the browser, and restore any earlier configuration.

```
# htpasswd -c /etc/httpd/testpass michael
```

# CERTIFICATION OBJECTIVE 14.04

# Regular and Secure Virtual Hosts

Perhaps the most useful feature of Apache is its ability to handle multiple web sites on a single IP address. In a world where there are no more new IPv4 addresses available, that can be useful. To do so, you can configure virtual hosts for regular web sites in the main Apache configuration file, /etc/httpd/conf/httpd.conf. In that way, you can configure multiple domain names such as www.example.com and www.mheducation.com on the same IP address on the same Apache server.

![](bbox=[0.1, 0.85, 0.22, 0.95])

> The example.com, example.org, and example.net domain names cannot be registered and are officially reserved by the Internet Engineering Task Force (IETF) for documentation. Many other example.* domains are also reserved by appropriate authorities.