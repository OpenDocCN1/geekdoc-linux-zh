+   2. Add these lines to the end of the file, since Apache reads things from the beginning to the end with the latter settings overriding the previous:

```
```
SSLEnable
SSLCacheServerPath        src/modules/ssl/gcache
SSLCacheServerPort        logs/gcache_port

SSLCertificateFile        /usr/local/ssl/certs/thawte_test.cert
SSLCertificateKeyFile     /usr/local/ssl/private/quasi.
                          gnuware.com.key

SSLVerifyClient    0
SSLVerifyDepth     2

SSLSessionCacheTimeout   300
```
```

+   3. Check the httpd.conf file on a working server and determine what you need to change. You may have to change the port number to 443 rather than port 80.

+   4. Start up the secure server by issuing the following command:
+   `/usr/local/etc/apache-ssl/httpd -f /usr/local/etc/apache-ssl/conf/httpsd.conf`.

+   5. Enter your PEM phrase when prompted.

If all seems well after you have completed these steps, you will be able to encode Web pages and transmit the information securely to yourself or others for processing.

# ## Conclusion

Now that you can set up network connections, you will be eager to create similar dial-up connections using your modem or cable-modem or any other device that connects to an ISP or another Linux box providing Internet connectivity. The next chapter will also look at the various programs used on Linux to connect to the Internet. Much like the many freeware programs that are available to Windows users, a plethora of Linux applications provides the same functionality for users of Linux, whether within an X session or on the console.