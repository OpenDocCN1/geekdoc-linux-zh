![](bbox=[0.22, 0.18, 0.78, 0.6])

Figure 2-3: You can configure the virtual host properties from this configuration window.

+   - **Server:** This tab has settings for the server such as the user and group names under which the HTTP server should run and the locations of the file where the process ID is stored.
+   - **Performance Tuning:** On this tab you can set some parameters that control overall performance. You can set the maximum number of connections allowed, the timeout period for connections, and the maximum number of requests per connection.

Initially the configuration window displays the default values from the configuration file `/etc/httpd/conf/httpd.conf`. After you make any changes, click the OK button. The configuration tool prompts you to ask whether you really want to save the changes and exit. If you do, click Yes and you should be done.

![](bbox=[0.12, 0.8, 0.2, 0.92])

When you configure the Apache HTTP server from this configuration tool, all you're doing is changing options and attributes stored in the `/etc/httpd/conf/httpd.conf` file. You can just as easily make the changes by editing the configuration file, which is a plain text file. In the next sections, I introduce you to some common configuration directives in the Apache configuration file.

# Apache configuration files

The Apache server's operation is controlled by the `httpd.conf` configuration file located in the `/etc/httpd/conf` directory. This file controls how the server runs, what documents it serves, and who can access these documents.

In the next few sections, I summarize key information about the `httpd.conf` configuration file. Typically, you don't have to change anything in the configuration files to run the Apache Web server. However, it's useful to