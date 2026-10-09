This returns a full configuration page for the server and all modules. If you wish to access it from a different location, use the fully qualified server name in place of localhost. For example, if your Web server is called www.nitec.com, you access the server information by using `http://www.nitec.com/server-info`.

The mod_info module also provides a directive called `AddModuleInfo`, which enables you to add descriptive text in the module listing provided by the mod_info module. The descriptive text could be anything including HTML text. AddModuleInfo has this syntax:

```
```
AddModuleInfo module_name descriptive_text
```
```

For example:

```
```
AddModuleInfo mod_info.c 'See <a
href="http://localhost/manual/mod/mod_info.html">man mod_info</a>'
```
```

This shows an HTML link next to the listing of mod_info.c, providing a quick way to get more information on the module from the Apache online manual, as shown below.

```
```
Module Name: mod_info.c
Content handlers: (code broken)
Configuration Phase Participation: Create Server Config, Merge Server Configs
Module Directives:
 AddModuleInfo - a module name and additional information on that module
 Current Configuration:
 AddModuleInfo mod_info.c 'man mod_info'
 Additional Information:
 man mod_info
```
```

You can also limit the information displayed on the screen as follows:

+   - ◆ **Server configuration only**. Use `http://server/server-info?server`, which shows the following information:
+   ```
+   Server Version: Apache/2.0.14 (Unix)
+   Server Built: Mar 14 2001 12:12:28
+   API Version: 20010224:1
+   Hostname/port: rhat.nitec.com:80
+   Timeouts: connection: 300 keep-alive: 15
+   MPM Information: Max Daemons: 20 Threaded: no Forked: yes
+   Server Root: /usr/local/apache
+   Config File: conf/httpd.conf
+   ```

+   - ◆ **Configuration for a single module**. Use `http://server/server-info?module_name.c`. For example, to view information on only the mod_cgi module, run `http://server/server-info?mod_cgi.c`, which shows the following information: