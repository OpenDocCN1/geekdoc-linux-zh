$Application->{Count}++;
$Application->Unlock();
%>
<h1> ASP Page </h1>
<hr>
<p>
This page has been called <%- $Application->{Count} %> times.
</body>
</html>

This simple test.asp ASP page simply increments the ASP Application object by one each time this page is called.

+   4. Add the following lines to the `httpd.conf` file:
+   `Alias /asp/ "/www/mysite/htdocs/asp"`
+   `<Location /asp/>`
+   `SetHandler perl-script`
+   `PerlHandler Apache::ASP`
+   `PerlSetVar Global /tmp`
+   `</Location>`

Here's what's going on in the preceding lines:

+   - The `/asp/` alias points to the `/www/mysite/htdocs/asp` directory. Make sure you change this so that it points to appropriate directory in your system.
+   - The `<Location>` container tells Apache to use the `Apache::ASP` module to handle all the files in this directory; it also sets the `Global` variable to the `/tmp` directory.
+   - The `Apache::ASP` module creates a directory called `/tmp/.state` in which it stores state information so that even if you shutdown and restart the server, the state information is not lost.

+   5. Change the file permissions for the `asp` directory and its contents to enable Apache user (i.e. allowing you set the User directive to in `httpd.conf`) to access the files. For example, use the `chown -R httpd:httpd /www/mysite/htdocs/asp` && `chmod -R 750 /www/mysite/htdocs/asp` commands to ensure that Apache user (httpd) and Apache group (httpd) can access the directory and files stored in it.

+   6. Restart the Apache server by using the `/usr/local/apache/bin/apachectl` restart command and access the `test.asp` page by using `http://your_server_name/asp/test.asp`.

![](bbox=[0.15, 0.93, 0.18, 0.98])

To learn more about how to write ASP scripts in Perl visit the ASP Web site at www.apache-asp.org.