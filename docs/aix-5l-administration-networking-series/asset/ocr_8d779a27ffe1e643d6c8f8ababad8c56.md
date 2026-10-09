IBM ships the Apache HTTP Server with the base operating system. Although several other Web servers run under AIX, Apache is now the Internet standard. The server’s job is to provide a common access interface to multimedia data and common Internet services. It does this via a combination of the Hypertext Transfer Protocol (HTTP) and the Hypertext Markup Language (HTML). HTML data pages residing on the server are transmitted to Web clients via HTTP. The Web server is responsible for maintaining access control to secured information and negotiating secure channels with Web clients.

The HTTP implementation resembles SMTP, the Internet mail protocol, in that it is a command/response-driven protocol that sends commands, data, and error codes on the same bidirectional socket connection. It also relies on MIME encoding documents to overcome self-imposed character set restrictions. These simple design choices aided in rapid implementation, widespread deployment, and the general popularity of the platform. Beyond simple HTML, the functionality of HTTP has been extended through the use of companion technologies, such as the programming languages JavaScript and Java. Extensible Markup Language (XML) and Extensible Stylesheet Language XSL are also helping transform the interworkings of the Web by differentiating between data and presentation elements.

# ## Apache Server Configuration

AIX includes a Web-based configuration system, which is accessible from the default server Web page. This configuration utilities run from an additional instance of the **httpd** daemon listening on network port 8008. This instance of the server must be started manually:

```
# /usr/HTTPServer/bin/httpd -f /usr/HTTPServer/conf/admin.conf
```

This configuration tool uses both Java and JavaScript for user interaction and can be helpful for quick installation of simple server configurations. However, the long chain of software and network dependencies that it requires makes it difficult to rely on. It is highly recommended that the competent Web administrator actually understand the details of Apache configuration.

The IBM-supplied binary distribution installs Apache into /usr/HTTPServer and organizes these resources into subdirectories (see Table 18-1).

# ## Directives Configuration

Apache contains a rich set of configuration options, controlled via “directives” that set either global or local values. Example 18-1 contains a listing of the first few directives in the **httpd.conf** file. Apache historically divided the configuration into three files: **srm.conf, access.conf, and httpd.conf**. The directives and data contained in these three files are now combined into **httpd.conf**. Support for **srm.conf** and **access.conf** is disabled by default by setting the **AccessConfig** and **ResourceConfig** directives to /dev/null (any number of arbitrarily named configuration files may be