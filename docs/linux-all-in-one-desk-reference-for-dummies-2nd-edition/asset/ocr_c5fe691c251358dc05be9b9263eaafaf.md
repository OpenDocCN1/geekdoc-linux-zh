Xandros, but in Debian, MEPIS, and Ubuntu it's named `apache2.conf`. The configuration file is a text file with directives that specify various aspects of the Web server.

![](bbox=[0.14, 0.2, 0.23, 0.3])

In Debian, MEPIS, SUSE, and Ubuntu, the configuration file is in the `/etc/apache2` directory. In Fedora Core, the `httpd.conf` file is in the `/etc/httpd/conf` directory. In Knoppix and Xandros, the file is in the `/etc/apache` directory.

The directory with the `httpd.conf` file also contains information about the Secure Sockets Layer (SSL) implementation needs. (The SSL implementation comes as part of the Apache Web server.)

# # Using Apache configuration tools

In some Linux distributions, you can use a GUI tool to configure the Apache Web server. In particular, Fedora Core and SUSE come with GUI tools for configuring the Apache Web server. I introduce you to these GUI tools in this section.

![](bbox=[0.14, 0.49, 0.23, 0.59])

In Fedora Core, log in as `root` and choose System Administration Server Settings HTTP from the GUI desktop. The HTTP dialog box appears, as shown in Figure 2-2.

![](bbox=[0.25, 0.57, 0.62, 0.81])

**Figure 2-2:**
In Fedora Core, configure the Apache HTTP server from this dialog box.

The Apache Configuration dialog box is organized into four tabs. You can set various options from each of these tabs:

+   **Main:** From this tab, you can specify the IP addresses and port number where Apache expects requests for Web service. You can also set the e-mail address of the Webmaster.