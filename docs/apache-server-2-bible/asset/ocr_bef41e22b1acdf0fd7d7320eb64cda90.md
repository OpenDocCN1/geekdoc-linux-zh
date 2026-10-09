```
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value.
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [GB]:US
State or Province Name (full name) [Some-State]:California
Locality Name (eg, city) []:Sacramento
Organization Name (eg, company) []:MyORG
Organizational Unit Name (eg, section) []:CS
server name (eg. ssl.domain.tld; required!!!)
[]:Shea_evoknow.com
Email Address []:kabi@evoknow.com
```

The certificate called `httpd.pem` is created in the `SSLConf/conf` subdirectory of your Apache source distribution.

You are now ready to configure Apache.

# ### Configuring Apache with Apache-SSL

When you ran `make install` in the “Compiling and Installing Apache-SSL Patches for Apache” section, it created an `httpd.conf` file in the `conf` subdirectory of your Apache installation directory. For example, if you used the `--prefix=/usr/local/apache` to configure Apache, you will find the `httpd.conf` file in `/usr/local/apache/conf` directory. You need to rename it to `httpd.conf` by using the `mv` command. Make sure you replace `/usr/local/apache/conf/` with the appropriate pathname if you installed Apache in a different directory.

You have two choices when it comes to using SSL with Apache. You can either enable SSL for the main server or you can enable it for one or more virtual Web sites. Here I show you how to enable SSL for your main Apache server and I also discuss what you need to do to enable SSL for a virtual Web site. Follow these steps to modify the `httpd.conf` file:

+   1. By default Web browsers will send SSL requests to port 443 of your Web server, so if you wish to turn the main Apache server into a SSL-enabled server, change the `Port` directive line to:
+   
+       Port 443
+       2. Add the following lines to tell Apache how to generate random data needed for encrypting SSL connections:
+   
+       SSLRandomFile file /dev/urandom 1024
+   SSLRandomFilePerConnection file /dev/urandom 1024
+       3. If you wish to reject all requests but the https (that is, SSL requests), insert the following directive:
+   
+   SSLRequireSSL