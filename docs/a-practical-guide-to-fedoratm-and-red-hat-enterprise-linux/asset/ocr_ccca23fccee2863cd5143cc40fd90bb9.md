+   13. Assume you want to provide Webmail access for employees on the same server that hosts the corporate Web site. The Web site address is example.com, you want to use mail.example.com for Webmail, and the Webmail application is located in /var/www/webmail. Describe two ways you can set up this configuration.

+   14. Part of a Web site is a private intranet. Describe how you would prevent people outside the company's internal 192.168.0.0/16 network from accessing this site. The site is defined as follows:

```
<VirtualHost ->
  ServerName example.com
  DocumentRoot /var/www
  <Directory /var/www/intranet>
      AllowOverride AuthConfig
  </Directory>
</VirtualHost>
```

+   15. What is a container? Give an example of container syntax.

+   16. What does CGI do? What are the characteristics of a CGI program?

+   17. What are the functions of SSL?