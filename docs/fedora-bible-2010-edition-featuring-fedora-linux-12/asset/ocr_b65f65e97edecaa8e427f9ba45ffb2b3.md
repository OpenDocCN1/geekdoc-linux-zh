There are many techniques you can use to secure your server (covered in Chapter 13), ranging from SELinux to certificates to controlling how scripts are run. Described here, however, are techniques for keeping an eye on the performance and security of your Apache Web server. Watching your server carefully can often stop an attack before it gets anywhere.

> **CAUTION:** You can often stop an attack before it occurs if you keep a close eye on your server. Use the techniques shown here to provide a high-level view of your server's status and then delve into the log files to make sure things are okay. Look for odd slow-downs, disks filling up, large numbers of requests, or odd patterns in the requests sent to your server. See Chapter 13 for more on system security.

Apache provides two unique built-in methods to check the performance and status of your Web server. The `server-status` handler can be configured to show information about server processes. The `server-info` handler can be configured to display a detailed summary of the Web server's configuration. You can activate these services by adding the following lines to the `/etc/httpd/conf/httpd.conf` file:

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1
</Location>

<Location /server-info>
    SetHandler server-info
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1
</Location>
```

In this example, all users from the local computer can display the `server-info` and `server-status` pages. You can change `127.0.0.1` to the name of any domain or host that your Apache server is hosting.

> **TIP:** If you want users to be able to put `localhost` in the URL, you need to add `localhost` as well as `127.0.0.1`.

# ## Displaying server information

The Server Information (`server-info`) page contains the server version information and various general configuration parameters and breaks up the rest of the data by module. Each loaded module is listed, with information about all directives supported by that module, and the current value of any defined directives from that module.

The Server Information is usually quite verbose and contains much more information than can be displayed in Figure 20-3, which shows only the links to each module's section and the general Server Settings section.