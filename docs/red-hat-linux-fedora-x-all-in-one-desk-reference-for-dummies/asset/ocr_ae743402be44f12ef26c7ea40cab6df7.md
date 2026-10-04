# Configuring the Apache Web Server 625

+   ServerAdmin is the e-mail address that the Web server provides to clients in case any errors occurs. The default value for ServerAdmin@ localhost. Set this address to a valid e-mail address that anyone on the Internet can use to report errors your site contains.

+   Include loads report directives from a specified file. For example, the default /etc/httpd/conf/httpd.conf loads all the configuration files from the /etc/httpd/conf.d directory by using the following Include directive:

Include conf/*.conf

This command means that you can load another set of configurations by simply adding a file to the /etc/httpd/conf.d directory. In fact, the directory where you find the configuration files for various Apache HTTPD modules as Perl, PHP, and SSL. Study the configuration file in the /etc/httpd/conf.d directory to find out about the total set of directives that affect the Apache server's behavior.

Many directives control the way that the Apache Web server works. The following list summarizes some of the directives you can use in the httpd.conf file. You can leave most of these directives in their default settings, knowing about them if you're maintaining a Web server is important.

+   Listen IP Address:Port: Forces the Web server to listen to a specific IP address and port number. The Web server responds to all IP addresses associated with the host.

+   Server name [#id]: Specifies the username (or ID) the HTTP daemon deons. You can leave this directive at the default setting (Apache). If you specify a user ID, use a hash (#) prefix for the numeric ID.

+   Group name [#id]: Specifies the group name (or ID) of the HTTP group when running in stand-alone mode. The default group name is apache.

+   ServerRoot pathname: Specifies the directory where the Web server is located. By default, the configuration and log files are located in subdirectories of this directory. In Fedora, ServerRoot is set to /etc/httpd.

+   ServerName www.company.com:80: Sets the server's host name to www.company.com and the port number to 80. ServerName is used when redirecting a Web page to another.

+   ServerTokens Major|Min|Prod|OS|Full: Controls how information is sent back to the client in the Server field of the header. Set the directive to Prod for a Server response that simply identifies the product name (in this case, Apache).

| Book VIII
Chapter 2 |
Running the Apache
Web Server |