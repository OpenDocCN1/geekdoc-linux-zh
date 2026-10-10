| Directive | What It Specifies |
| :--- | :--- |
| `Listen 80` | Apache daemon will listen for HTTP requests on port 80. |
| `ServerName server1.class.com` | Name of the local server is server1.class.com. |
| `DocumentRoot "/var/www/html"` | Document root directory is /var/www/html on the local computer. |
| `DirectoryIndex index.html` | Index.html file in the document root directory will be sent to clients who request an HTML document. |
| `ServerRoot /etc/httpd` | All paths listed within the /etc/httpd/conf/httpd.conf file are relative to the /etc/httpd directory. |
| `ErrorLog logs/error_log` | All Apache daemon messages will be written to the /etc/httpd/logs/error_log file. |
| `CustomLog logs/access_log combined` | All Web requests will be written to the /etc/httpd/logs/access_log file using a combined log format. |
| `MaxClients 150` | Maximum number of simultaneous requests cannot exceed 150. |
| `User apache` | Apache daemon will run as the “apache” local user account. |
| `Group apache` | Apache daemon will run as the “apache” local group account. |
| `<Directory "/var/www/html">`<br>`Order allow,deny`<br>`Allow from all`<br>`Deny from 192.168.1.51`<br>`</Directory>` | All hosts are allowed to access HTML files and other Web content from the /var/www/html directory except for the computer with the IP address 192.168.1.51. |

Table 13-2 Common httpd.conf directives

The default settings in the httpd.conf file are sufficient for most simple Web servers; thus, you simply need to copy the appropriate HTML files to the /var/www/html directory, including the index.html file, start Apache to host Web content on your network, and ensure that Apache is started automatically at boot time. Client computers can then enter the location http://servername_or_IPaddress in their Web browser to obtain the default Web page. Each time a client request is received by the Apache Web server (called a Web page hit), a separate httpd daemon is started to service the request.

![](bbox=[0.12, 0.8, 0.89, 0.92])

On a busy Web server, there may be several hundred httpd daemons running on the system responding to client requests. The first httpd daemon is started as the root user and is used to start all other httpd daemons. These non-root httpd daemons are started as a regular user account to prevent privileged access to the system. For example, the User apache directive