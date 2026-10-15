The Web server normally sets up your Web site in the /var/www directory. It also sets up several directories for managing the site. The /var/www/cgi-bin directory holds the CGI scripts, and /var/www/html/manual holds the Apache manual in HTML format. You can use your browser to examine it. Your Web pages are to be placed in the /var/www/html directory. Place your Web site home page there. Your configuration files are located in a different directory, /etc/httpd/conf. Table 22-2 lists the various Apache Web server directories and configuration files.

To upgrade your Apache server, either use the Red Hat upgrade tool (RHN) or look for recent Apache update files at the Red Hat FTP site. For binary versions for an RPM supported distribution Red Hat, you can download RPM packages containing the latest version of the Apache Web server, specially configured for your Red Hat Linux distribution. For Red Hat, the RPM packages for the Apache Web server are now named httpd instead of apache. Alternatively, you can download the source code version for the latest Apache Web server directly from Apache and compile it on your system. You must decompress the file and extract the archive. Many of the same directories are created, with added ones for the source code. The server package includes installation instructions for creating your server directories and compiling your software. Make sure the configuration files are set up and installed.

> NOTE If you are installing Apache from the source code, notice that versions of the configuration files ending with the extension .conf-dist are provided. You have to make copies of these configuration files with the same prefix, but only with the extension .conf to set up a default configuration. The Web server reads configuration information only from files with a .conf extension.

| Web Site Directories | Description |
|---|---|
| /var/www | Directory for Apache Web site files on Red Hat systems |
| /var/www/html | Web site Web files |
| /var/www/cgi-bin | CGI program files |
| /var/www/html/manual | Apache Web server manual |
| Configuration Files | |
| .htaccess | Directory-based configuration files: an .htaccess file holds directives to control access to files within the directory in which it is located |
| /etc/httpd/conf | Directory for Apache Web server configuration files |
| /etc/httpd/conf/httpd.conf | Apache Web server configuration file |
| /etc/httpd/conf/conf.d | Directory holding module configuration files like ssl.conf for SSL and php.conf for PHP |
| Startup Scripts | |
| /etc/rc.d/init.d/httpd | Startup script for Web server daemon |

# TABLE 22-2 Apache Web Server Files and Directories (RPM Installation)