# ### EXERCISES

+   1. How would you tell Apache that your content is in **/usr/local/www**?
+   2. How would you instruct an Apache server to listen on port 81 instead of port 80?
+   3. How would you enable Sam to publish Web pages from his ~/website directory but not allow anyone else to publish to the Web?
+   4. Apache must be started with **root** privileges. Why? Why does this action not present a security risk?

# ### ADVANCED EXERCISES

+   5. If you are running Apache on a firewall system, perhaps to display a Web front-end for firewall configuration, how would you make sure that it is accessible only from inside the local network?
+   6. Why is it more efficient to run scripts using **mod_php** or **mod_perl** than to run them through CGI?
+   7. What two things does SSL provide and how does this situation differ if the certificate is self-signed?
+   8. Some Web sites generate content by retrieving data from a database and inserting it into a template using PHP or CGI each time the site is accessed. Why is this practice often a poor idea?
+   9. Assume you want to provide Webmail access for employees on the same server that hosts the corporate Web site. The Web site address is example.com, you want to use mail.example.com for Webmail, and the Webmail application is located in /var/www/webmail. Describe two ways you can set up this configuration.
+   10. Part of a Web site is a private intranet. Describe how you would prevent people outside the company's internal 192.168.0.0/16 network from accessing this site. The site is defined as follows:

```
<VirtualHost *> 
    ServerName example.com
    DocumentRoot /var/www
    <Directory /var/www/intranet>
      AllowOverride AuthConfig
    </Directory>
</VirtualHost>
```