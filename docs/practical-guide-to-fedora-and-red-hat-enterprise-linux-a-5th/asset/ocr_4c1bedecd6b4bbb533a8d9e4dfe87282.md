http://example.org. The browser should display the Fedora/RHEL/Apache test page. This test page is actually an error page that says there is no content. For more information refer to “Fedora/RHEL test page” on page 872.

If the server is behind a firewall, open TCP port 80 (page 844). If you are having problems getting Apache to work, see “Troubleshooting” on page 875.

# PUTTING YOUR CONTENT IN APACHE

Place the content you want Apache to serve in /var/www/html. Apache automatically displays the file named index.html in this directory. Working as root (or as a member of the group you set up for this purpose [e.g., webwork]), give the following command to create such a page:

```
```bash
#  cat >  /var/www/html/index.html
<html><body><p>This is my test page.</p></body></html>
CONTROL-D
```
```

After creating this file, either refresh the browser if it is still running or start it again and point it at the server. The browser should display the page you just created.

# JUMPSTART II: SETTING UP APACHE

# Using system-config-htpd

# Make a copy of httpd.conf

> tip As installed, the /etc/httpd/conf/httpd.conf file contains extensive comments and is set up as explained in this chapter. The system-config-htpd utility overwrites this file. Make a copy of httpd.conf for safekeeping before you run this utility for the first time.

You can use the system-config-htpd utility to display the HTTP window, which allows you to edit the /etc/httpd/conf/httpd.conf file to set up Apache. To run this utility, enter system-config-htpd on a command line or select Main menu: System -> [Server Settings ->] Administration -> HTTP.

The HTTP window has four tabs: Main, Virtual Hosts, Server, and Performance Tuning. Each field in these tabs/windows corresponds to a directive in the /etc/httpd/conf/httpd.conf file. This section discusses some of the basic directives you can change with system-config-htpd. For more information click Help at the bottom of the HTTP window.

The Main tab (Figure 26-1) allows you to establish an FQDN (page 1083) as the name of the server (ServerName, page 852), an email address for the server administrator (ServerAdmin, page 851) and the ports and addresses that Apache listens on for requests (Listen, page 851). Highlight an entry in the Available Addresses subwindow, and click Edit to edit that entry or Add to add a new entry. Both