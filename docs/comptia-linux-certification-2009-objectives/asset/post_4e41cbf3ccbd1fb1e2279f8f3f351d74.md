
![](img/477ccb2f05b6ba1b2d563ea74f18c197_635_0.png)

Figure 13-10: Downloading a file using the curl command.

## Syntax

The syntax of the curl command is `curl [options] {URL...}`.

## Application Servers

An application server is a server program running on a computer connected to a distributed network. It makes the most of an application program that is accessible across the network. An application server makes custom applications available to multiple concurrent users. It can also be used to develop, run, and manage applications. It consists of three tiers: the first-tier GUI, the middle-tier business logic, and the third-tier database and transaction server.

## Tomcat

Tomcat is an open source application server that implements a Java servlet and renders JavaServer pages. It provides a Java HTTP web server environment for Java code to run on a Linux system. Tomcat can run programs in response to user requests and send the dynamic results to users. Tomcat possesses an internal web server, which is useful while running multiple applications. It can be used along with other web servers such as Apache, Sun Java System Web Server, and Microsoft Internet Information Server.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_636_0.png)

Figure 13-11: The Tomcat application homepage on a Linux system.

## Java Servlets

A Java Servlet is a Java object file that is developed as a component and can be run on a server. Because a servlet is a Java program, it enables you to exploit the full power of Java within web applications. It allows you to access Java class library functions such as network connections and database access. The servlet is a component and can be invoked from HTML, Java Server Page, or by another servlet. Because the Java servlet can be invoked from an HTML document, it provides the HTML page with powerful server-side processing capability.

## Containers

A container, also called web engine or web container, is a special web server that supports the execution of servlets. It combines the basic function of a web server with java-specific optimization and extensions. It translates specific URLs into servlet requests. A container contains information such as the functionality and URL of registered servlets. This information is used to uniquely identify servlets and deliver service requests to the appropriate servlets. Servlets can be added to and removed from the container without affecting the running servlets. Tomcat is a example of a servlet container.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_636_1.png)

## How to Configure a Web Server

### Procedure Reference: Install Apache

To install Apache:

1. Log in as root.
2. Mount the Linux installation media that contains Apache.
3. Navigate to the `/media/name of the media/Server` directory.
4. Install the dependency packages for Apache.
   - a. Enter `rpm -ivh apr-(version).(release).rpm`.
   - b. Enter `rpm -ivh postgresql-libs-(version).(release).rpm`.
   - c. Enter `rpm -ivh apr-util-(version).(release).rpm`.
5. Enter `rpm -ivh httpd-(version).(release).rpm` to install Apache.
6. Enter `rpm -qi httpd` to verify that Apache has been installed.
7. If necessary, enter `umount /media/cdrom` to unmount the installation CD.

### Procedure Reference: Configure the Apache Web Server

To configure the Apache web server:

1. Log in as root.
2. Using the vi editor, open the httpd.conf file.
   - Open the httpd.conf file from the `/etc/httpd/conf` directory when Apache is installed using RPM.
   - Open the httpd.conf file from the `[/Installation Directory]/conf` directory when Apache is installed from a user source.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_637_0.png)

3. Locate the ServerAdmin statement and enter the email address of the webmaster.
   `ServerAdmin (email address)`
4. Locate the ServerName option and then enter the IP address of the web server.
   `ServerName (IP address: Port)`
5. Locate the DocumentRoot option and enter the path of the directory that is used to serve web content.
   `DocumentRoot (Absolute path of the web content directory)`
6. Locate the DirectoryIndex option and enter the list of index files for the directory.
   `DirectoryIndex (List of index files)`
7. Save and close the file.
8. Enter `service httpd start` to start the httpd service for the configuration changes to take effect.
9. Enter `chkconfig httpd on` to enable the httpd service during system startup.

Update the DNS zone file if you want to use hostnames for the web server.

### Procedure Reference: Tune the Apache Server

To tune the Apache server:

1. Log in as root.
2. Using the vi editor, open the `/etc/httpd/httpd.conf` file.
3. Set the Apache configuration settings to tune the server.
   - Locate the MaxKeepAliveRequests directive and specify the maximum number of requests that are allowed.
   - Locate the StartServers directive and set the initial number of server processes.
   - Locate the MinSpareServers directive and specify the minimum number of spare servers.
   - Locate the MaxSpareServers directive and specify the maximum number of spare servers.
   - Locate the MaxClients directive and specify the maximum number of client connections that run in parallel.
   - Locate the KeepAlive directive and set it to On or Off to allow or prevent more than one request per connection.
   - Locate the KeepAliveTimeout directive and specify the time limit for a request with respect to the connection.
4. Save and close the file.
5. Enter `service httpd configtest` to test the configuration file.
6. Enter `service httpd restart` to restart the httpd service for the configuration changes to take effect.

### Procedure Reference: Configure the Apache Namespace

To configure the Apache namespace:

1. Log in as root.
2. Using the vi editor, open the `/etc/httpd/conf/httpd.conf` file.
3. Locate the UserDir option and uncomment the line to allow users to allocate a separate space for their web content.
4. Uncomment the directory section defined for the home directory to control access to UserDir directories.

```apache
<Directory /home/user_name/public_html>
  AllowOverride FileInfo AuthConfig Limit
  Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
  <Limit GET POST OPTIONS>
    Order allow,deny
    Allow from all
  </Limit>
  <LimitExcept GET POST OPTIONS>
    Order deny,allow
    Deny from all
  </LimitExcept>
</Directory>
```

5. Save and close the file.
6. Enter `mkdir /home/user_name/public_html` to create a directory for the web content.
7. Copy the user's own web content into `/home/{user name}/public_html`.
8. Enter `chown -R user_name:User_group /home/user_name` to change the ownership permission of the user's home directory.
9. Enter `chmod -R 755 /home/user_name` to change the permissions of the user's home directory.
10. Enter `service httpd configtest` to test the configuration file.
11. Enter `service httpd restart` to restart the httpd service for the configuration changes to take effect.
12. Access the website and verify the configuration.
    `http://localhost/~user_name`

### Procedure Reference: Configure the Apache Log

To configure the Apache log:

1. Log in as root.
2. Using the vi editor, open the `/etc/httpd/conf/httpd.conf` file.
3. Locate the `ErrorLog` statement and specify the location where error logs should be stored.
   `ErrorLog (location of error logs)`
4. Locate and specify the `CustomLog` directive.
   - a. Specify a log format by using the `LogFormat` directive.
     `LogFormat "format" format_name`
   - b. Define a `CustomLog` directive that uses the log format you created.
     `CustomLog logs/access_log format_name`

![](img/477ccb2f05b6ba1b2d563ea74f18c197_639_0.png)

5. Enter `service httpd configtest` to check whether the `httpd.conf` file is configured correctly.
6. Enter `service httpd restart` to restart the `httpd` service for the configuration changes to take effect.
