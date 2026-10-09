# ## Access Control

After data transfer, access control is probably the most important function of the Web server. Access control limits the capabilities of both Web clients and Web page publishers primarily according to location and identity. In the example shown in Example 18-4, access control is first strictly limited in one scope and then relaxed in another to meet administrative objectives. One directive scope can be a subset of another, which effectively overrides the former for some branch of the uniform resource identifier (URI) tree.

# ### Example 18-4

```
DocumentRoot /usr/HTTPServer/htdocs/en_US/
<Directory />
Options FollowSymLinks
AllowOverride none
</Directory>
<Directory /usr/HTTPServer/htdocs/en_US>
Options Indexes FollowSymLinks
AuthType basic
AuthName "Web Server Access Control"
AuthUserFile conf/UsersAndPasswords
Require valid-user
</Directory>
```

The first `Directory` block sets the default access rules for the default document root: Publishers are permitted to map objects from the filesystem into the URI space recognized by the server; they are, however, unable to override any subsequent access control via .htaccess files. The second `Directory` block enables basic user authentication for the whole document tree. The `AuthUserFile` directive defines the user database file location.

The simple `AuthUserFile` database is a colon-delimited text file of user IDs and hashed passwords, similar to the UNIX `/etc/passwd` file. On servers with many users, searching this file can become a performance problem. The `AuthDBUserFile` directive can be used instead to speed up this process. The `htpasswd` and `dbmmanage` utilities are used to populate the respective user files.

Both of these authorization schemes offer minimal real security, because the passwords are passed across the network as “cleartext,” readable by anyone capable of sniffing the network connection. Keep this in mind when implementing a basic authentication scheme for your Web site; a least make sure the server is outside of a firewall and otherwise isolated on the network from sensitive systems. For more serious security, use the Secure Sockets Layer (SSL) protocol, also supported by Apache HTTP Server.