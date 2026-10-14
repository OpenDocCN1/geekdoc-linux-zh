Save the file and exit. Now it's time to try out your proxy server. First of all, start it. To do that, follow these steps:

+   1. Log in as root.
+   2. Change the directory to /sbin/init.d.
+   3. Start squid by running the following command:
+      ```
+      # ./squid start
+      ```
+   4. That's it, squid is now started.

The next thing is to configure your browser to use the proxy server. You can easily do this by following these steps:

+   1. Run your Netscape browser.
+   2. Click the Edit menu, and click Preferences at the bottom of the menu.
+   3. The Preferences dialog appears. Click Advanced, Proxies.
+   4. Click Manual Proxy Configuration.
+   5. Click the View button. The View Manual Proxy Configuration dialog appears.
+   6. Enter 127.0.0.1 in the HTTP Proxy field.
+   7. Enter 3128 in the Port field (see Figure 22.2). If you changed the default port number in squid's configuration file, enter the new one instead.

# FIGURE 22.2
Setting up Netscape to use the proxy server.

![](bbox=[0.28, 0.7, 0.62, 0.88])

+   8. Repeat the previous step with the FTP Proxy fields.
+   9. Close all the dialogs.

Your browser is now ready to use the proxy server. Test it by typing in any URL. The browser will contact the proxy server, asking it to fetch that URL. The server will then fetch it, save a local copy, and return another to the browser. As time passes and your use of the proxy server increases, the pages will load more quickly. This is because squid has cached them on your local disk drive for fast access.