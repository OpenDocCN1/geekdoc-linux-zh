
## ACTIVITY 13-1
### Configuring a Web Server

**Before You Begin:**

- On srvA, you have logged in as root in the GUI.
- The terminal window is displayed.
- Enter `cd /root` to navigate to the root directory.
- On the terminal window, copy the `english.html` file and the `Our Global Company_files` directory from the `/085039Data/Web_Services` directory to the `/var/www/html` directory.
- Clear the terminal window.

**Scenario:**

Your company runs a chain of retail stores and wants to set up an online web store, which will provide information about the store and facilitate online shopping. Now, you want to configure the web server to facilitate web hosting. Also, you want to configure the web server in such a way that PHP pages are included in the website.

### What You Do

| Step | Action |
| :--- | :--- |
| 1. | Check whether httpd has been installed on the system. |
| a. | Verify that the apr package has been installed on the system. |
| b. | Verify that the postgresql-libs package has been installed on the system. |
| c. | Verify that the apr-util package has been installed on the system. |
| d. | Verify that the httpd package has been installed on the system. |
| e. | Clear the terminal window. |
| 2. | Enable PHP support on the system. |
| a. | Enter `yum localinstall /rhelsource/Server/=> php-common-5.1.6-23.el5.i386.rpm` to install the php-common package. <br> **Note:** The `=>` symbol is used in the step only to bring the step to the next line. It is not part of the code and therefore, students need not type the symbol. |
| b. | Enter `yum localinstall \ /rhelsource/Server/=> \ php-cli-5.1.6-23.el5.i386.rpm` to install the php-cli package. <br> **Note:** The `⇒` symbol is used in the step only to bring the step to the next line. It is not part of the code and therefore, students need not type the symbol. |
| c. | Enter `yum localinstall \ /rhelsource/Server/=> \ php-5.1.6-23.el5.i386.rpm` to install the php package. <br> **Note:** The `⇒` symbol is used in the step only to bring the step to the next line. It is not part of the code and therefore, students need not type the symbol. |
| d. | Clear the terminal window. |
| 3. | Specify alias names for the web server. |
| a. | Navigate to the /var/named directory. |
| b. | Using the vi editor, open the ogc.forward file. |
| c. | At the end of the file, type `www IN CNAME srvA` to add a CNAME record. |
| d. | Press Esc to switch to the command mode. |
| e. | Save and close the file. |
| f. | Restart the named service. |
| g. | Clear the terminal window. |
| 4. | Configure the web server to allow web hosting. |
| a. | Navigate to the /etc/httpd/conf directory. |
| b. | Using the vi editor, open the httpd.conf file. |
| c. | Locate the line “#ServerName www.example.com:80” and change it to **ServerName www.ourglobalcompany.com:80** |
| d. | Press **Esc** to switch to the command mode. |
| e. | Locate the “<Directory “/var/www/html”>” statement. |
| f. | Locate the line **AllowOverride None** in the <Directory “/var/www/html”> statement. |
| g. | Change the **AllowOverride None** parameter to **AllowOverride AuthConfig** |
| h. | Press **Esc** to switch to the command mode. |
| i. | Locate the line “DirectoryIndex index.html index.html.var” and change it to **DirectoryIndex english.html english.html.var** |
| j. | Press **Esc** to switch to the command mode. |
| k. | Save and close the file. |
| l. | Clear the terminal window. |
| 5. | Start the httpd service to apply configuration changes. |
| a. | Enter **service httpd start** to start the httpd service. |
| b. | Enter **chkconfig httpd on** to start the httpd service when the system boots. |
| c. | Clear the terminal window. |
| 6. | Access the website that you have set up. |
| a. | Enter `firefox http://ourglobalcompany.com` to open the website in the Firefox browser. |
| b. | Observe that the homepage of Our Global Company is displayed in the Mozilla Firefox web browser. |
| c. | Close the web browser window. |
| d. | Clear the terminal window. |

## TOPIC B
### Implement Apache Access Control

You configured a web server. You may need to host multiple websites on a single web server and secure it to restrict unauthorized access. In this topic, you will implement Apache access control.

Your organization may have intranet sites for employees. Because the number of users accessing the intranet sites will be fewer when compared to the Internet websites, you decide to host both websites on the same server. To do so, you will need to use security methods to segregate data for the two sites. As a system administrator, it is also essential to ensure the general security of data stored on the server. Therefore, you will need the skills to set up access control appropriately.

### Virtual Hosts

![](img/477ccb2f05b6ba1b2d563ea74f18c197_645_0.png)

**Definition:**
A *virtual host* is a system that enables management of more than one domain. It can have more than one domain or IP address. The virtual host can be name based or IP based. The `VirtualHost` directive is used to define a virtual machine. Details, such as the IP address, web page information, log format, and domain name, are specified in the httpd.conf file.

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_645_1.png)

*Figure 13-12: A list of domains managed by the virtualhost system.*

### IP-Based Virtual Hosting

IP-based virtual hosting enables multiple websites based on IP addresses to be hosted by a system. The server will be assigned to more than one IP address, and each IP address will point to a website. To define an IP-based virtual host, the IP address of the web server should be specified in the `VirtualHost` directive.

### Name-Based Virtual Hosting

Name-based virtual hosting is a method by which a system can host more than one website based on the host name. In this method, many hosts can have the same IP address. This method is preferred to host multiple websites on the same web server. The server will be assigned to more than one host name and each host name will point to a website. A name-based virtual hosting can be configured using the `NameVirtualHost` directive. The IP addresses of the hosts that need to be served are specified in the `NameVirtualHost` directive, provided the IP addresses are associated with a network interface on the server. In addition, the server can be made to listen or restrict the IP address specified in the `NameVirtualHost` directive using the `Listen` or `BindAddress` directive, respectively. The `NameVirtualHost` directive is followed by the `VirtualHost` directive defined for each host that needs to be served.

### The Transport Layer Security Protocol

**Definition:**

*Transport Layer Security (TLS), the third version of Secure Sockets Layer (SSL), is a protocol that provides secure communication between servers and clients. TLS establishes a secure communication channel between a server and a client and then encrypts all data that needs to be communicated. TLS uses cryptography to provide authentication and securely transfer data. The `mod_ssl` is the Apache module that is used for enabling TLS and SSL on the Apache server. The `ssl.conf` configuration file is stored in the `/etc/httpd/conf.d` directory. It is used to provide TLS support to the Apache server.*

![](img/477ccb2f05b6ba1b2d563ea74f18c197_646_0.png)

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_646_1.png)

*Figure 13-13: Secured communication between the server and the client.*

### Digital Certificates

*A digital certificate is a digital document that authenticates a specific public key belonging to an individual or a company. It contains the individual's name or the company name, the serial number, the expiration dates, a copy of the certificate holder's public key, and the digital signature of the certificate issuing authority. Digital certificates can be self-signed or signed by a Certificate Authority (CA). They are required to set up a secure web server. The digital certificate is stored in the `/etc/pki/tls/certs` directory.*

![](img/477ccb2f05b6ba1b2d563ea74f18c197_646_2.png)
