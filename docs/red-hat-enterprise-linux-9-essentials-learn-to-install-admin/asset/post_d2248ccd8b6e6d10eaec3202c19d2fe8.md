
## 29.3 Configuring the Firewall

Before starting and testing the Apache web server, the firewall must be modified to allow the webserver to communicate with the outside world. By default, the HTTP and HTTPS protocols use ports 80 and 443, respectively, so depending on which protocols are being used, either one or both of these ports will need to be opened. When opening the ports, be sure to specify the firewall zone that applies to the internet-facing network connection:

```
# firewall-cmd --permanent --zone=<zone> --add-port=80/tcp
# firewall-cmd --permanent --zone=<zone> --add-port=443/tcp
```

After opening the necessary ports, be sure to reload the firewall settings:

```
# firewall-cmd --reload
```

On cloud-hosted servers, enabling the appropriate port for the server instance within the cloud console may also be necessary. Check the documentation for the cloud provider for steps to do this.

## 29.4 Port Forwarding

Suppose the RHEL 9 system hosting the web server sits on a network protected by a firewall (another computer running a firewall, router, or wireless base station containing built-in firewall protection). In that case, you must configure the firewall to forward ports 80 and 443 to your web server system. The mechanism for performing this differs between firewalls and devices, so check your documentation to find out how to configure port forwarding.

## 29.5 Starting the Apache Web Server

Once the Apache server is installed and the firewall configured, the next step is to verify that the server is running and start it if necessary.

To check the status of the Apache service from the command line, enter the following at the command prompt:

```
# systemctl status httpd
```

If the above command indicates that the httpd service is not running, it can be launched from the command line as follows:

```
# systemctl start httpd
```

If you would like the Apache httpd service to start automatically when the system boots, run the following command:

```
# systemctl enable httpd
```

## 29.6 Testing the Web Server

Once the installation is complete, the next step is verifying the web server is running.

If you have access (either locally or remotely) to the desktop environment of the server, start up a web browser and enter http://127.0.0.1 in the address bar (127.0.0.1 is the loop-back network address which tells the system to connect to the local machine). If everything is set up correctly,

the browser should load the test page shown in Figure 29-1:

![](img/be1f159c3cc937d7b264dc5b134856dc_237_0.png)

Figure 29-1

If the desktop environment is unavailable, connect either from another system on the same local network as the server, or use the external IP address assigned to the system if it is hosted remotely.

## 29.7 Configuring the Apache Web Server for Your Domain

The next step in setting up your web server is configuring it for your domain name. To configure the web server, begin by changing directory to /etc/httpd, which, in turn, contains several files and sub-directories. Change directory into the conf sub-directory, where you will find a file named httpd.conf containing the configuration settings for the Apache server.

Edit the httpd.conf file using your preferred editor with super-user privileges to ensure you have permission to access and modify the file. Once loaded, several settings need to be changed to match your environment.

The most common way to configure Apache for a specific domain is to add virtual host entries to the httpd.conf file. This allows a single Apache server to support multiple websites simply by adding a virtual host entry for each site domain. Within the httpd.conf file, add a virtual host entry for your domain as follows:

```
<VirtualHost *:80>
    ServerAdmin feedback@myexample.com
    ServerName www.myexample.com
    DocumentRoot /var/www/myexample
    ErrorLog logs/myexample_error_log
    CustomLog logs/myexample_access_log combined
</VirtualHost>
```

The ServerAdmin directive in the above virtual host entry defines an administrative email address for people wishing to contact the webmaster for your site. Change this to an appropriate email address where you can be contacted.

Next, the ServerName is declared so the web server knows the domain name associated with this virtual host.

Since each website supported by the server will have its own set of files, the DocumentRoot setting is used to specify the location of the files for this website domain. The tradition is to use /var/www/domain-name, for example:

```
DocumentRoot  /var/www/myexample
```

Finally, entries are added for the access history and error log files.

Create the /var/www/<domain name> directory as declared in the httpd.conf file and place an index.html file in it containing some basic HTML. For example:

```
<html>
<title>Sample Web Page</title>
<body>
Welcome to MyExample.com
</body>
</html>
```

The last step is to restart the httpd service to make sure it picks up our new settings:

```
# systemctl restart httpd
```

Finally, check that the server configuration works by opening a browser window and navigating to the site using the domain name instead of the IP address. The web page that loads should be defined in the index.html file created above.

## 29.8 The Basics of a Secure Website

The web server and website created in this chapter use the HTTP protocol on port 80 and, as such, are considered to be insecure. The problem is that the traffic between the web server and the client (typically a user's web browser) is transmitted in clear text. In other words, the data is unencrypted and susceptible to interception. While not a problem for general web browsing, this is a severe weakness when performing tasks such as logging into websites or transferring sensitive information such as identity or credit card details.

These days, websites are expected to use HTTPS, which uses either Secure Socket Layer (SSL) or Transport Layer Security (TLS) to establish secure, encrypted communication between a web server and a client. This security is established through the use of public, private, and session encryption together with certificates.

To support HTTPS, a website must have a certificate issued by a trusted authority known as a Certificate Authority (CA). When a browser connects to a secure website, the web server sends back a copy of the website's SSL certificate, which also contains a copy of the site's public key. The browser then validates the authenticity of the certificate with trusted certificate authorities.

If the certificate is valid, the browser uses the public key sent by the server to encrypt a session key and pass it to the server. The server decrypts the session key using the private key to send an encrypted acknowledgment to the browser. Once this process is complete, the browser and server use the session key to encrypt all subsequent data transmissions until the session ends.

## 29.9 Configuring Apache for HTTPS

By default, the Apache server does not include the necessary module to implement a secure HTTPS website. The first step, therefore, is to install the Apache mod_ssl module on the server system as follows:

```
# dnf install mod_ssl
```

Restart httpd after the installation completes to load the new module into the Apache server:

```
# systemctl restart httpd
```

Check that the module has loaded into the server using the following command:

```
# httpd -M | grep ssl_module
ssl_module (shared)
```

Once the ssl module is installed, repeat the steps from the previous section of this chapter to create a configuration file for the website, this time using the sites-available/default-ssl.conf file as the template for the site configuration file.

Assuming the module is installed, the next step is to generate an SSL certificate for the website.

## 29.10 Obtaining an SSL Certificate

The certificate for a website must be obtained from a Certificate Authority. Several options are available at a range of prices. By far the best option, however, is to obtain a free certificate from Let's Encrypt at the following URL:

https://letsencrypt.org/

Obtaining a certificate from Let's Encrypt involves installing and running the Certbot tool. This tool will scan the Apache configuration files on the server and provides the option to generate certificates for any virtual hosts configured on the system. It will then generate the certificate and add virtual host entries to the Apache configuration for the corresponding websites.

Follow the steps on the Let's Encrypt website to download and install Certbot on your RHEL 9 system, then run the certbot tool as follows to generate and install the certificate:

```
# certbot --apache
```

After requesting an email address and seeking terms of service acceptance, Certbot will list the domains found in the httpd.conf file and allow the selection of one or more sites for which a certificate will be installed. Certbot will then perform some checks before obtaining and installing the certificate on the system:

```
Which names would you like to activate HTTPS for?
------------------------------------------------------------
1: www.myexample.com
```
