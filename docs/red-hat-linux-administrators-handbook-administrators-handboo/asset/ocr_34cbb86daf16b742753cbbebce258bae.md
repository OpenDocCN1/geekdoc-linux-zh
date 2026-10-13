ument. On the other hand, if the HTTP_USER_AGENT does not contain the MSIE string, it is assumed to be the other leading browser, Netscape Navigator, and thus the browser variable is set to "Navigator" and the javascript.html file is inserted in the current document. By using the if-then-else construct, this example sets a different value to the same variable and loads different files.

# Hosting virtual Web sites

Apache supports two types of virtual hosts — IP-based virtual hosts and name-based virtual hosts. No matter what type of virtual host you choose to implement, proper Domain Name Service (DNS) configuration is a prerequisite. IP-based virtual host configuration requires unique IP addresses for each virtual host, and name-based virtual hosts are created using CNAME records.

# Apache configuration for virtual hosts

You can configure Apache in two ways to enable it to support multiple hosts (the main server and the virtual servers):

+   - Run multiple daemons, so that each host has a separate httpd daemon.
+   - Run a single daemon that supports all the virtual hosts and the primary server host.

The second approach is widely used and preferable in most cases. Hence, only this method is discussed in this section.

A single httpd daemon launches child processes to service requests for the primary Web site and all the virtual sites; by default, Apache listens to port 80 on all IP addresses of the local machine, and this is often sufficient. If you have a more complex requirement, such as listening on various port numbers or listening only to specific IP addresses, the BindAddress or Listen directive can be used.

Apache uses the special container <VirtualHost> in the httpd.conf file to handle all the virtual host-specific configurations. An example of a minimal virtual host configuration might look like this:

```
<VirtualHost 192.168.0.50>
```