# DIRECTIVES YOU MIGHT WANT TO MODIFY AS YOU GET STARTED

When it starts, Apache reads the /etc/httpd/conf/httpd.conf configuration file (by default) for instructions governing every aspect of how Apache runs and serves content. The httpd.conf file shipped with Fedora/RHEL is more than 350 lines long. This section details some directives you might want to change as you start using Apache. You can add/modify each of the following directives in httpd.conf. The Context line in each explanation tells you which locations the directives can appear in; contexts are explained on page 945. The section titled “Advanced Configuration Directives” on page 949 describes more directives.

+   *   **Listen**  *Specifies the IP address and port that Apache listens for requests on.*
+       Listen [IP-address:]portnumber
+       where **IP-address** is the IP address that Apache listens on and **portnumber** is the number of the port that Apache listens on for the given IP-address. When IP-address is absent or is set to 0.0.0.0, Apache listens on all network interfaces. At least one Listen directive must appear in the configuration files or Apache will not work.
+       The following minimal directive from the httpd.conf file listens for requests on all network interfaces on port 80:
+       `Listen 80`
+       The next directive changes the port from the default value of 80 to 8080:
+       `Listen 8080`
+       When you specify a port other than 80, each request to the server must include a port number (as in www.example.org:8080) or the kernel will return a **Connection Refused** message. Use multiple Listen directives to have Apache listen on multiple IP addresses and ports. For example:
+       `Listen 80`
+       `Listen 192.168.1.1:8080`
+       `Listen 192.168.1.2:443`
+       accepts connections on all network interfaces on port 80, on 192.168.1.1 on port 8080, and on 192.168.1.2 on port 443.
+       Context: **server config**
+       Default: none (Apache will not start without this directive.)
+       Fedora/RHEL: Listen 80

+   *   **Redirect**  *Tells the client to fetch a requested resource from a different, specified location.*
+       Redirect [status] requested-path [new-URL]
+       where status is the status that Apache returns along with the redirect. If you omit status, Apache assumes temp. The status can be an Apache error code in the range 300–399 or one of the following: