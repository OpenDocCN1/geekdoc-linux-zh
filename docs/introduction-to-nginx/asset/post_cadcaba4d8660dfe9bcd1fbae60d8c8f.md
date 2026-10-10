
![](img/3adf2b91cc40e3d0012eab041f055ca8_46_0.png)

Figure 4.7: screenshot

The test.php file was served by the CentOS 6.4 server.

We will go ahead and edit the nginx.conf file again (see Figs. 4.8 and 4.9).

```nginx
upstream app_rack {
    #ip_hash;
    server 10.0.2.13:8080 max_fails=3 fail_timeout=30s;
    server 10.0.2.14:8080 weight=3;
    # backup can only be used if ip_hash is not present
    server 127.0.0.1:8080 down;
}
```

Figure 4.8: The requests will be served by either the Debian or the CentOS server

```nginx
upstream app_rack {
    #ip_hash;
    server 10.0.2.13:8080 down; # max_fails=3 fail_timeout=30s;
    server 10.0.2.14:8080 weight=2 down;
    # backup can only be used if ip_hash is not present
    server 127.0.0.1:8080 backup;
}
```

Figure 4.9: Since The Debian and CentOS servers have marked as down, all the requests will be forwarded to the local Ubuntu 12.04 server

With the upstream block show in Fig. 4.9, the php file will be served by the Ubuntu server (see Fig. 4.10)

![](img/3adf2b91cc40e3d0012eab041f055ca8_47_0.png)

Figure 4.10: The php file is served by the Ubuntu server, which is marked as backup

Now, say that we have an application (running on the 3 servers) that is drawing high traffic. How can we know which server is receiving each request from the frontend server? That is where the embedded variable `$upstream_addr`-which is built-into the upstream module- and the `log_format` directive come into play.

- Define a custom `log_format` (`MyLogFormat` in the example below) at http level in the main configuration file (see Fig. 4.11)

```nginx
http {
    include        mime.types;
    default_type   application/octet-stream;
    #access_log    logs/access.log  main;
    sendfile       on;
    keepalive_timeout  65;

    log_format MyLogFormat '$upstream_addr [$time_local] - $http_referer';

    upstream app_rack {
```

Figure 4.11: Creating a custom log format

- Use the log format created earlier with one of the logs (see Fig. 4.12)

```nginx
server {
    listen        80;
    server_name   nginxtest.com;
    root          /home/gacanepe/nginx-1.5.6/html;
    access_log    /home/gacanepe/nginx-1.5.6/html/access_log MyLogFormat;
    error_log     /home/gacanepe/nginx-1.5.6/html/error_log;
    location / {
        index    index.html index.htm;
    }
}
```

Figure 4.12: Adding a custom log format to the access log

Now let's modify the upstream block once again (see Fig. 4.13) in order to forward traffic to the 3 servers.

```nginx
upstream app_rack {
    #ip_hash;
    server 10.0.2.13:8080; # max_fails=3 fail_timeout=30s;
    server 10.0.2.14:8080 weight=2;
    # backup can only be used if ip_hash is not present
    server 127.0.0.1:8080;
}
```

Figure 4.13: Modifying the upstream block in order to forward requests to the three backend servers

Now restart Nginx and, finally, let's see what the access log shows (see Fig. 4.14) after refreshing the browser's windows a couple of times:

```bash
gacanepe@ubuntuOS:~/nginx-1.5.6/html$
tail -f access_log
10.0.2.14:8080 [08/Nov/2013:11:16:50 -0300] - -
127.0.0.1:8080 [08/Nov/2013:11:16:50 -0300] - http://localhost/test.php
10.0.2.13:8080 [08/Nov/2013:11:16:50 -0300] - http://localhost/test.php
10.0.2.14:8080 [08/Nov/2013:11:17:02 -0300] - -
10.0.2.14:8080 [08/Nov/2013:11:17:02 -0300] - http://localhost/test.php
10.0.2.13:8080 [08/Nov/2013:11:17:02 -0300] - http://localhost/test.php
127.0.0.1:8080 [08/Nov/2013:11:17:07 -0300] - -
10.0.2.14:8080 [08/Nov/2013:11:17:07 -0300] - http://localhost/test.php
10.0.2.13:8080 [08/Nov/2013:11:17:07 -0300] - http://localhost/test.php
```

Figure 4.14: The access log

## 4.3 Download the configuration file

You can download the configuration file of this tutorial: LoadBalance_conf.zip

## Chapter 5

Nginx SSL configuration guide

### 5.1 Introduction

The SSL (Secure Socket Layer) protocol was created by Netscape to ensure secure transactions between web servers and browsers (using secure pages often identified with https://). The protocol uses a third party, a Certificate Authority (CA), to identify one end or both ends of the transactions (The Linux Documentation Project).

### 5.2 Adding support for SSL to Nginx

Since The Linux Documentation Project website offers a comprehensive explanation of how this procedure is performed, we will limit this tutorial to show how to set up SSL with Nginx on Ubuntu 12.04 LTS. We will need to compile Nginx with SSL support (see Fig. 5.1).

![](img/3adf2b91cc40e3d0012eab041f055ca8_50_0.png)

However, the ssl module requires the OpenSSL library (see Fig. 5.2) to be installed on the system beforehand. We will install the libssl-dev package, which includes the said library (see Fig. 5.3).

![](img/3adf2b91cc40e3d0012eab041f055ca8_50_1.png)

```bash
gacanepa@ubuntuOS:~$ sudo aptitude install libssl-dev
[sudo] password for gacanepa:
The following NEW packages will be installed:
  libssl-dev libssl-doc[zlib-dev]
0 packages upgraded, 3 newly installed, 0 to remove and 150 not upgraded.
Need to get 2,620 kB of archives. After unpacking 6,773 kB will be used.
Do you want to continue? [Y/n/?] Y
WARNING: untrusted versions of the following packages will be installed!

Untrusted packages could compromise your system's security.
You should only proceed with the installation if you are certain that
this is what you want to do.

  libssl-dev libssl-doc zlib-dev

Do you want to ignore this warning and proceed anyway?
To continue, enter "Yes"; to abort, enter "No": Yes
```

Figure 5.3: Installing the libssl-dev package, which provides the OpenSSL library

### 5.3 Creating, signing, and using a certificate

- We will create a directory to store our public key and ssl certificate (see Fig. 5.4).

```bash
gacanepa@ubuntuOS:~$ sudo mkdir /usr/local/nginx/ssl
[sudo] password for gacanepa:
gacanepa@ubuntuOS:~$  
```

Figure 5.4: Creating a directory to store the public key and ssl certificate

- Now let’s generate the server private key (see Fig. 5.5)

```bash
gacanepa@ubuntuOS:/usr/local/nginx/ssl$ sudo openssl genrsa -out server.key 1024
Generating RSA private key, 1024 bit long modulus
.....................................+++++++++
............................+++++++++
e is 65537 (0x10001)
gacanepa@ubuntuOS:/usr/local/nginx/ssl$ ls -l
total 4
-rw-r--r-- 1 root root 887 Nov  8 15:50 server.key
gacanepa@ubuntuOS:/usr/local/nginx/ssl$
```

Figure 5.5: screenshot

- Create a certificate signing request (see Fig. 5.6)

![](img/3adf2b91cc40e3d0012eab041f055ca8_52_0.png)

Figure 5.6: screenshot

- Sign your certificate (see Fig. 5.7). Please note that this certificate will only last one day (you can modify this setting by changing the argument to the -days option).

![](img/3adf2b91cc40e3d0012eab041f055ca8_52_1.png)

Figure 5.7: Signing your ssl certificate

- Set up the certificate. Edit the nginx.conf file (see Fig. 5.8). Note that even though there is a ssl directive (ssl on | off) available, it is recommended to use the ssl parameter of the listen directive instead of this directive.

```nginx
server {
 listen 443 ssl;
 server_name nginxTest.com;
 root /home/gacanepa/nginx-1.5.6/html;
 access_log /home/gacanepa/nginx-1.5.6/html/access_log MyLogFormat;
 error_log /home/gacanepa/nginx-1.5.6/html/error_log;
 ssl_certificate /usr/local/nginx/ssl/server.crt;
 ssl_certificate_key /usr/local/nginx/ssl/server.key;
 location / {
 index index.html index.htm;
 }
}
```

Figure 5.8: screenshot

It should be kept in mind that due to the HTTPS protocol limitations virtual servers should listen on different IP addresses (see Fig. 5.9). Refer to the nginx.conf file to perform the following modifications if needed:

```nginx
server {
 listen 192.168.1.1:443;
 server_name one.example.com;
 ssl_certificate /usr/local/nginx/conf/one.example.com.cert;
 ... 
}

server {
 listen 192.168.1.2:443;
 server_name two.example.com;
 ssl_certificate /usr/local/nginx/conf/two.example.com.cert;
 ... 
}
```

Figure 5.9: screenshot

Otherwise the first server's certificate will be issued for the second site.

In order to allow to share a single IP address between multiple HTTPS servers is to use a certificate with a wildcard name, for example, *.example.org. A wildcard certificate secures all subdomains of the specified domain, but only on one level. This certificate matches www.example.org, but does not match example.org and www.sub.example.org. These two methods can also be combined. A certificate may contain exact and wildcard names in the SubjectAltName field, for example, example.org and *.example.org.

If we want to allow Subject Alternative Names (SANs) for our certificates we need to enable the following options in the file openssl.cnf file (located in /etc/ssl/openssl):

1. Include the X509 Version 3 (RFC 2459) extension to allow an SSL certificate to specify multiple names that the certificate should match. We need the [ req ] section to read as follows (see Fig. 5.10). This tells openssl to include the v3_req section while generating certificate requests:
