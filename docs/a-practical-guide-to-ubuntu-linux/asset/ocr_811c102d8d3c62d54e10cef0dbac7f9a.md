# INTRODUCTION 901

For example, installing phpmyadmin(sourceforge.net/projects/phpmyadmin) makes it available to a browser as /phpmyadmin.

This section describes the packages you need to install and provides references for the programs covered in this chapter. The “Notes” section introduces terminology and other topics that may help you make better sense of this chapter. The JumpStart section (page 903) gets Apache up and running as quickly as possible.

# MORE INFORMATION

+   - Local Apache HTTP Server Version 2.2 Documentation: With Apache running apache-2 doc installed, point a browser at server/manual, where server is localhost or the name or IP address of the Apache server.
- Apache directives: server/manual/mod/directives.html
- SSI directives: server/manual/howto/ssl.html
- Web Apache documentation: http.apache.org/docs/2.2
- Apache directives: http.apache.org/docs/2.2/mod/directives.html
- Apache Software Foundation (newsletters, mailing lists, projects, module registry, and more): www.apache.org
- webalizer: www.murunix.net/webalizer
- awstats: awstats.sourceforge.org
- libapache2-mod-perl: perl.apache.org (mod_perl)
- libapache2-mod-php5: www.php.net (mod_php)
- libapache2-mod-python: www.modpython.org (mod_python)
- SSL: modssl.org (mod_ssl)
- MRTG: mrtg.hartld/mrtg
- SNMP: net-snmp.sourceforge.net
- SSI directives: http.apache.org/docs/2.2/howto/ssl.html

# NOTES

+   - Terms: Apache and apache2 Apache is the name of a server that serves HTTP and other content. The name of Apache 2 daemon is apache2.
- Terms: server and process An Apache server is the same as an Apache process. An Apache child process exists to handle incoming client requests; it is referred to as a server.
- Firewall An Apache server normally uses TCP port 80; a secure server uses TCP port 443. If the Apache system is running or behind a firewall, you must open one or both of these ports. To get started, open port 80 (HTTP). Using gufw (page 876), open these ports by setting a policy that allows service for HTTP and or HTTPS.
- Running with root privileges Because Apache serves content on privileged ports, you must start running with privileges. For security reasons, Ubuntu sets Apache to spawn processes that run as the user and group www-data.
- Locale The apache2 daemon starts with the C locale by default. You can modify this behavior—for example, by using the configured system locale—setting the LANG variable in the /etc/init.d/apache2 file. (in the line that starts with ENV=-i LANG= ...) in the /etc/init.d/apache2 file.