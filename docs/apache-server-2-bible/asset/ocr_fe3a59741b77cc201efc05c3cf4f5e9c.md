# Configuring Apache for mod_ssl-based SSL

If you compile **mod_ssl** with Apache after you have already built Apache once, the SSL-related configuration directives are stored in **httpd.conf.default** instead of in **httpd.conf**. Basically, when you add **mod_ssl** on an existing Apache server, the **httpd.conf** file is preserved. You must manually configure the SSL-related directives by copying necessary information from **httpd.conf.default**. In the following material, I assume that you are adding **mod_ssl** to a preexisting Apache system by recompiling Apache with **mod_ssl** support as shown in the previous section. To configure Apache for SSL by using **mod_ssl**, follow these steps:

+   1.  If you installed **mod_ssl** as a shared module, then add the following line in **httpd.conf**:
+   
+       AddModule \_ssl\_module modules/libssl.so

+   2.  Modify **httpd.conf** so that it includes these directives:
+   
+       ```
+       <IfDefine SSL>
+           Listen 80
+           Listen 443
+       </IfDefine>
+       ```
+   
+       This **\<IfDefine\>** container tells Apache to consider the enclosed directives only if Apache was started with **-DSSL** option or **apachectl startssl** was used. In SSL mode, Apache is told to listen for connection on the standard **HTTP** port 80 and also on the standard **HTTPS** port 443.

+   3.  Add the following lines in **httpd.conf** to tell Apache to add two MIME types for **.crt** and **.crl** extensions. The first extension denotes a certificate file and the second denotes a certificate revocation list (CRL) file. These two lines ensure that Apache sends the appropriate header when sending files with these extensions.
+   
+       ```
+       <IfDefine SSL>
+           AddType application/x-x509-ca-cert .crt
+           AddType application/x-pkcs7-crl .crl
+       </IfDefine>
+       ```

+   4.  Add the following lines to the **httpd.conf** to define the SSL session cache database path, the cache timeout value, the SSL mutex file path used by SSL-enabled children to communicate, the SSL random-seed-generation method, the SSL log path, and the SSL log level information.
+   
+       ```
+       <IfModule mod_ssl.c>
+   
+           SSLPassPhraseDialog builtin
+   
+           SSLSessionCache dbm:/usr/local/apache/logs/ssl_scache
+           SSLSessionCacheTimeout 300
+   
+           SSLMutex file:/usr/local/apache/logs/ssl_mutex
+   
+           SSLRandomSeed startup builtin
+       ```