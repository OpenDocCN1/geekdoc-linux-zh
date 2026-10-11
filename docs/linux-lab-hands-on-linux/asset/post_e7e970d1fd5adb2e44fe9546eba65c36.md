
## 1. Starting Apache

Use the following commands to start Apache at boot:

```bash
[root@netmon tmp]# chkconfig --level 345 httpd on
[root@netmon tmp]# service httpd start
[root@netmon tmp]# service httpd stop
[root@netmon tmp]# service httpd restart
```

## 2. Test the Apache Process

Use the following command to test the Apache process:

```bash
[root@netmon tmp]# pgrep httpd
```

## 3. Test from the Client

Open a browser and type the URL of the server. (If you are not able to configure the DNS server, use `http://ipaddress_server`). You will get a default Apache web page.

## 4. Modifying the httpd.conf File (/etc/httpd/conf/httpd.conf)

Basic Settings:

Suggested modifications in the httpd.conf file.

-   **i. ServerName Directive:**
    Change the default value for `ServerName` to `www.<your-domain.com>` or `ServerName` to the IP address of the server if the DNS server is not configured.
    ```apache
    ServerName domain-name (or ipaddress of server if dns server is not configured.)
    ```

-   **ii. DocumentRoot Directive:**
    Put the website content in `/var/www/html` (This is the HTML directory).

    Test from the client: Open a browser and type the URL of the server. If you did not configure a DNS server, use `http://ipaddress_server`. You will get the web page of the website placed in the document root directory.

## Virtual Hosting

### Named Virtual Hosting

Multiple websites share a single IP address.

Go to the VirtualHost Directive:

1.  Write the server name of different websites in the VirtualHost directive.
2.  In order to host multiple websites on a single Apache server, create document directories for them.
3.  Use the following commands to create document directories to host multiple websites on a single Apache server:

    ```bash
    [root@netmon tmp]# cd /var/www/html
    [root@netmon html]# pwd
    [root@netmon html]# mkdir site1
    [root@netmon html]# mkdir site2
    ```

    Put the web pages of different websites into these directories. Use the following commands to copy or link the web pages into the directories:

    ```bash
    [root@netmon tmp]# cd /var/www/html/site1
    [root@netmon site1]# ln -s index.htm index.html
    ```

    Configure `httpd.conf` for Name Virtual Hosting:

    ```apache
    NameVirtualHost 172.16.10.26

    <VirtualHost *>
        # Default Directives. (in other words, not site #1 or site #2)
    </VirtualHost>

    <VirtualHost 172.16.10.26>
        ServerName www.site1.org
        # Directives for site #1
    </VirtualHost>

    <VirtualHost 172.16.10.26>
        ServerName www.site2.org
        # Directives for site #2
    </VirtualHost>
    ```

### IP-Based Virtual Hosting

The other virtual hosting option is to have one IP address per website, which is also known as IP-based virtual hosting.

Assigning multiple IP addresses to a single Ethernet interface:

```bash
[root@netmon tmp]# ifconfig eth0:0 10.10.10.1 netmask 255.0.0.0 up
```

Check the IP address:

```bash
[root@netmon tmp]# ifconfig eth0
```

## IP Virtual Hosting Example

In this example, Apache listens on all interfaces, but gives different content for addresses 172.16.10.26 and 10.10.10.1. Web surfers get the site1 content if they try to access the web server on any of its other IP addresses.

```apache
<VirtualHost *>
    DocumentRoot /home/www/site1
</VirtualHost>

<VirtualHost 172.16.10.26>
    DocumentRoot /home/www/site2
</VirtualHost>

<VirtualHost 10.10.10.1>
    DocumentRoot /home/www/site3
</VirtualHost>
```

Test from the client:
Open a browser and type the URL of the servers.

1.  `http://172.16.10.26`
    You will get a web page of the first website.
2.  `http://172.16.10.1`
    You will get a web page of the second website.

## Summary

In this chapter, you learned to install and configure the Apache (httpd) Server. You also learned about Virtual Hosting.

## 18 LAB: Configuring Proxy Server (SQUID)

### OBJECTIVES

1.  Install and configure Squid proxy server.
2.  Restrict Web Access by IP and Time.
3.  Squid Proxy Server Authentication.
4.  Monitoring Squid Proxy Server.

### REQUIREMENTS

PC with Pentium IV class processor, 1-GB RAM, 80 GB HDD, NIC, with installed FC6 or RHEL 5 etc.

### CONCEPT

A proxy server sits between a web server and a web client (browser) and acts as a gateway between the two. There are many advantages to having a proxy server. The main ones are:

-   **Security:** The ability to allow or deny access to external web servers using Access Control Lists (ACLs).
-   **Accounting:** Logging all of your clients' access to the internet. Reports and statistics can be generated from these logs.
-   **Caching:** Frequently accessed pages are cached locally and shared by all local web clients. This saves bandwidth on your internet connection.

Let's learn about Squid files and directories.

## SQUID Files and Directories

-   `/etc/squid/`: Contains the Squid configuration files.
-   `/var/spool/squid`: Contains the Squid cache.
-   `/var/log/squid`: Contains the Squid logs.

Let's now learn about the Squid proxy server in detail.

## SQUID Proxy Server

Squid is a high-performance caching proxy server. Proxy servers are used to cache data streams such as FTP, HTTP, and gopher. Network clients can then be directed to the proxy server to aid in pulling up cached HTTP documents.

Users configure their web browsers to use the Squid proxy server instead of going to the web directly. The Squid server then checks its web cache for the web information requested by the user. It returns any matching information that it finds in its cache. If it does not find any, it goes to the web to find it on behalf of the user. Once it locates the information, Squid populates its cache with that information and also forwards it to the user’s web browser.

This reduces the amount of data accessed from the web. Another advantage is that you can configure your firewall to accept HTTP web traffic from the Squid server only and no one else. Squid can then be configured to request usernames and passwords for each user that uses its services. This provides simple access control to the internet.

Let’s now learn about installing the Squid proxy server.

## Installing Squid Proxy Server

For installing the Squid proxy server, you need to use the RPM package. Let’s install the Squid proxy server using the Squid package.

### Install the Squid Package

Check the Linux distribution CD/DVD for the Squid RPM package.

```bash
[root@netmon tmp]# rpm -ivh squid-ver-release-arch.rpm
```

This command installs the Squid package. Let’s now learn to start the Squid server.

### Starting Squid

Use `chkconfig` to configure Squid to start at boot:

```bash
[root@netmon tmp]# chkconfig --level 35 squid on
```

Use the `service` command to start, stop, and restart Squid after booting:

```bash
[root@netmon tmp]# service squid start
[root@netmon tmp]# service squid stop
[root@netmon tmp]# service squid restart
```

You can test whether the Squid process is running with the `pgrep` command:

```bash
[root@netmon tmp]# pgrep squid
```

You should get a response of plain old process ID numbers.

### SQUID Basic Configuration

The basic Squid configuration file is stored in `squid.conf` in the `/etc/squid` directory. Let’s now learn the Squid configuration.

-   The `/etc/squid/squid.conf` file is the Squid configuration file.

Open the file using a text editor and type the following command to open the Squid configuration file:

```bash
[root@netmon tmp]# vi /etc/squid/squid.conf
```

In the Squid configuration file, the default access control lists (ACLs) appear. You need to define your own ACL (Access Control List) to work with Squid. The default port is TCP 3128. The following example ACL allows access from your local network 172.16.0.0/16. Make sure you adapt the list to include your internal IP networks from where browsing should be allowed:

```apache
acl our_network src 172.16.0.0/16
http_access allow our_network
```

### The Visible Host Name

Squid will fail to start if you don't give your server a hostname. You can set this with the `visible_hostname` parameter. Here, the hostname is set to the real name of the server `netmon`.

```apache
visible_hostname netmon
```

Save and close the file and start the Squid proxy server. Type the following command to start the Squid proxy server:

```bash
[root@netmon tmp]# chkconfig -level 35 squid on
[root@netmon tmp]# /etc/init.d/squid start
```

Output:

```text
Initializing cache dir: /var/spool/squid... Starting squid: [ OK ]
```

Verify port 3128 is open:

```bash
[root@netmon tmp]# netstat -tulnp | grep 3128
tcp 0 0 0.0.0.0:3128 0.0.0.0:* LISTEN
```

![Open TCP port 3128](img/f3b9cff79e19317416c12eaf5ded7245_182_0.png)

Finally, make sure iptables is allowing access to the Squid proxy server. Just open the `/etc/sysconfig/iptables` file:

```bash
[root@netmon tmp]# vi /etc/sysconfig/iptables
```

Append the following configuration:

```bash
-A RH-FireWall-1-INPUT -m state --state NEW,ESTABLISHED,RELATED -m tcp -p tcp --dport 3128 -j ACCEPT
```

Restart the iptables firewall:

```bash
[root@netmon tmp]# /etc/init.d/iptables restart
```
