the Web site or to inform the administrator of problems. There is no default value for ServerAdmin; if you do not use this directive, and ServerSignature is set to EMail, the mailto: link on error pages displays [no address given].

# ServerAdmin attracts spam

The email address you put in ServerAdmin often attracts spam. Use a spam-guarded address such as “nmg at sobell dot com” (you must use the quotation marks) or use a custom error page to point to a Web page with a form for sending mail to the right person.

You can use a role alias such as webmaster at your domain and use a mail alias to forward mail that is sent to webmaster to the person who is responsible for maintaining the Web site. See the discussion of mail aliases on page 746.

+   * Contexts: server config, virtual host
+   * Default: none
+   * Fedora/RHEL: root@localhost

# ServerName Specifies the server’s name and the port it listens on.

```
ServerName FQDN [:-port]
```

where FQDN is the fully qualified domain name or IP address of the server and -port is the optional port number Apache listens on. The domain name of the server must be able to be resolved (by DNS or /etc/hosts) and might differ from the hostname of the system running the server. If you do not specify a ServerName, Apache performs a DNS reverse name resolution (page 862) on the system’s IP address and assigns that value to ServerName. If the reverse lookup fails, Apache assigns the system’s IP address to ServerName.

Fedora/RHEL provides the following ServerName template in the httpd.conf file:

```
#ServerName www.example.com:80
```

Copy this line, remove the #, and substitute the FQDN or IP address of the server for www.example.com. You can omit the :80 because it specifies the default port. Change the 80 to the port number Apache listens on if it does not listen on port 80. The ports specified by ServerName and Listen (page 940) must be the same if you want the FQDN specified by ServerName to be tied to the IP address specified by the Listen directive.

Apache uses ServerName to construct a URI when it redirects a client (page 962). See also UseCanonicalName (page 951).

+   * Contexts: server config, virtual host
+   * Default: none
+   * Fedora/RHEL: none

# DocumentRoot Points to the root of the directory hierarchy that holds the server’s content.

```
DocumentRoot dirname
```