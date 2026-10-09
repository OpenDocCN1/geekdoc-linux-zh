
## ACTIVITY 13-2
Maintaining a Web Server

**Before You Begin:**

1. On srvA, you have logged in as root in the GUI.
2. The terminal window is displayed.
3. Create a directory named *german* in the `/var/www` directory.
4. Copy the *german.html* file from the `/085039Data/Web_Services` directory to the `/var/www/german` directory.
5. Clear the terminal window.

**Scenario:**

OGC Systems is planning to expand its operations globally. As part of its expansion strategy, the company devised various strategies to establish its presence in new markets. One of the plans is to host an official website in different languages for its widespread customer base, so that it can reach out to a wider audience. The web design team designed the German version of the customer website, and you want to use the existing web server to host the new website. You also want to ensure that the new website is accessible only to customers in that specified region.

| What You Do | How You Do It |
|:--- |:--- |
| 1. Specify alias names for the web server. | a. Navigate to the `/var/named` directory. <br> b. Using the *vi* editor, open the *ogc.forward* file. <br> c. At the end of the file, type <br> *german IN CNAME srvA* to add a CNAME record. <br> d. Press **Esc** to switch to the command mode. <br> e. Save and close the file. <br> f. Restart the *named* service. <br> g. Clear the terminal window. |
| 2. Add VirtualHost directives to the English and German websites. | a. Using the vi editor, open the /etc/httpd/conf/httpd.conf file. <br> b. At the end of the file, enter `NameVirtualHost 192.168.0.2` to specify the IP address of the web server. <br> c. Enter `<VirtualHost www.ourglobalcompany.com>` to begin the first VirtualHost directive. <br> d. Enter `ServerName 192.168.0.2` to specify the IP address of the server. <br> e. Enter `DocumentRoot /var/www/html` to specify the directory where the HTML files will be stored. <br> f. Enter `DirectoryIndex english.html` to specify the file. <br> g. Enter `</VirtualHost>` to complete the VirtualHost directive. <br> *See Code Sample 1.* <br> h. Add a `VirtualHost` directive with the server name `german.ourglobalcompany.com` and Document Root location `/var/www/german`. <br> *See Code Sample 2.* <br> i. Press **Esc** to switch to the command mode. <br> j. Save and close the file. <br> k. Restart the httpd service. <br> l. Clear the terminal window. |
| 3. Create users who can access your website. | a. Navigate to the /var/www/html directory. <br> b. Enter <br> **httpasswd -mc** <br> **/var/www/html/.htpasswd webuser** <br> to create the webuser user. <br> c. Enter **@webuser1** as the password. <br> d. When prompted, retype **@webuser1** <br> e. Observe that the password for webuser is added. <br> f. Enter **chgrp apache .htpasswd** to specify that apache is the group owner of the password file. <br> g. Enter **chmod g+r .htpasswd** to provide group read permission for the password file. |
| 4. Configure Apache to authenticate users. | a. Using the vi editor, open the .htaccess file. <br> b. Enter Authname "This is a trusted website." to specify the message to be displayed in the authentication dialog box. <br> c. Enter Authuserfile "/var/www/html/.htpasswd" to indicate the name of the file that contains details about users who have access to the website. <br> d. Enter Authtype basic to specify the type of authentication. <br> e. Type require valid-user to specify that all valid users can access the website. <br> *See Code Sample 3.* <br> f. Press Esc to switch to the command mode. <br> g. Save and close the file. <br> h. Clear the terminal window. |
| 5. Check whether you are able to access the English and German versions of the website. | a. Enter **firefox** **http://ourglobalcompany.com** to open the website in the Firefox web browser. <br> b. In the **Authentication Required** dialog box, in the **User Name** text box, type **webuser** and press the **Tab** key. <br> c. In the **Password** text box, type **@webuser1** and then press the **Tab** key and **Enter**. <br> d. On the toolbar, click **Never for This Site** to prevent Firefox from prompting you to save the password. <br> e. Close the web browser window. <br> f. Enter **firefox** **http://german.ourglobalcompany.com** to open the German website in the web browser. <br> g. Observe that the home page of the German version of Our Global Company is displayed. <br> h. Close the web browser window. <br> i. Clear the terminal window. |

Code Sample 1

```
NameVirtualHost 192.168.0.2
<VirtualHost www.ourglobalcompany.com>
ServerName 192.168.0.2
DocumentRoot /var/www/html
DirectoryIndex english.html
</VirtualHost>
```

Code Sample 2

```
<VirtualHost german.ourglobalcompany.com>
ServerName 192.168.0.2
DocumentRoot /var/www/german
DirectoryIndex german.html
</VirtualHost>
```

Code Sample 3

```
Authname "This is a trusted website."
Authuserfile "/var/www/html/.htpasswd"
Authtype basic
require valid-user
```

## TOPIC C

### Implement Access Control in a Proxy Server

You implemented web services on your network. It is now critical to ensure that only authorized users are allowed to access websites through the server. In this topic, you will configure a proxy server.

According to the organization policy, you may have to provide the Internet access to all employees. However, inappropriate usage of the Internet can affect server performance. Therefore, you may want to restrict user access to certain websites and monitor the usage with the help of a proxy server.

### Proxy Servers

**Definition:**

A *proxy server* is a server that acts as an intermediary between a web browser and a web server. It contains cache information of the web server and intercepts all requests sent to the web server. A proxy server comprises a main server utility, programs for performing authentication, and management tools. The proxy server supports data transmitted through HTTP, FTP, and Gopher protocols.

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_657_0.png)

*Figure 13-16: Data transmission occurring through a proxy server.*

### The Squid Server

Squid is a proxy server that is used for caching Internet data. When a client requests data, Squid accepts the request and forwards it to a remote server, which is the original server, or to another proxy server. Squid receives the data, stores a copy of it in the cache, and then sends it to the respective client machine. The copy of the data that is stored in the cache is used to serve client requests in the future. The caches can be arranged in a hierarchy using the light-weight Internet Cache Protocol (ICP). Squid supports data transfer using FTP, HTTP, Gopher, and SSL protocols.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_658_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_658_1.png)

The Squid web server is referred to as a web accelerator. In such instances, it serves one or more dynamic documents apart from serving some static documents and operates faster, thereby optimizing server and network performance. It protects the original web server from being attacked by external data and invalid URLs because it hides the original web server.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_658_2.png)

### ICP

ICP is a protocol that is used for coordinating and communicating among web caches. It queries proxy servers for caches.

### Gopher

The Gopher protocol is a TCP/IP application layer protocol that is used to search and retrieve documents from the Internet.

### The squid.conf File

The squid.conf file, stored in the /etc/squid directory, is the main configuration file used to configure Squid. The squid daemon runs from the /usr/sbin directory and listens on port 3128. The initialization script runs from the /etc/init.d/squid file. By default, the squid.conf file contains tags that are used to set parameters to the server.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_659_0.png)

There are various parameters defined in the squid.conf file. Each parameter is set to a value that defines the server functionality. Some parameters are described in the table below.

| Parameter | Description |
| :--- | :--- |
| cache_mem | Specifies the amount of memory that Squid will use for caching popular requests. By default, it is set to 8 MB. |
| maximum_object_size | Specifies the maximum size of the cache. |
| minimum_object_size | Specifies the minimum size of the cache. |
| cache_dir | Specifies the type of storage system and the directory name where the cache files are stored. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_659_1.png)
