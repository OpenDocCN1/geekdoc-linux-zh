![](bbox=[0.05, 0.08, 0.13, 0.15])

Update the DNS zone file if you want to use hostnames for the web server.

# **Procedure Reference: Tune the Apache Server**

To tune the Apache server:

+   1.  Log in as root.
2.  Using the vi editor, open the /etc/httpd/httpd.conf file.
3.  Set the Apache configuration settings to tune the server.

+      - Locate the MaxKeepAliveRequests directive and specify the maximum number of requests that are allowed.
   - Locate the StartServers directive and set the initial number of server processes.
   - Locate the MinSpareServers directive and specify the minimum number of spare servers.
   - Locate the MaxSpareServers directive and specify the maximum number of spare servers.
   - Locate the MaxClients directive and specify the maximum number of client connections that run in parallel.
   - Locate the KeepAlive directive and set it to On or Off to allow or prevent more than one request per connection.
   - Locate the KeepAliveTimeout directive and specify the time limit for a request with respect to the connection.

+   4.  Save and close the file.
5.  Enter service httpd configtest to test the configuration file.
6.  Enter service httpd restart to restart the httpd service for the configuration changes to take effect.

# **Procedure Reference: Configure the Apache Namespace**

To configure the Apache namespace:

+   1.  Log in as root.
2.  Using the vi editor, open the /etc/httpd/conf/httpd.conf file.
3.  Locate the UserDir option and uncomment the line to allow users to allocate a separate space for their web content.