```
acl admin src 192.168.1.0/255.255.255.0
acl lunch time MTWHF 12:00-13:00
http_access allow myhosts
http_access allow lunch
http_access deny admin
visible_hostname srvA.ourglobalcompany.com
```

+   2.     Deny access to pornographic sites.

+   a.     Enter `acl restricted_site urlpath_regex -i porn` to create the `restricted_site` ACL.

+   b.     Enter `http_access deny restricted_site` to deny access to the `restricted_site` ACL.

> See Code Sample 2.

+   c.     Press `Esc` to switch to the command mode.

+   d.     Save and close the file.

+   e.     Enter `service squid start` to start the Squid service.

+   f.     Clear the terminal window.

Code Sample 2

```
http_access deny admin
acl restricted_site urlpath_regex -i porn
**http_access deny restricted_site**
```