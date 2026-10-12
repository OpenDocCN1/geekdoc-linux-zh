# Using a dedicated user and group for Apache

If you run Apache as a standalone server, create a dedicated user and group for Apache. Do not use the nobody user or the nogroup group, especially if your system has already defined these. Chances are good that your system is using them for other services or in other places. This might lead to administrative and security problems. Instead, create a fresh new user and group for Apache, and use them with the User and Group directives.

# Protecting ServerRoot and log directories

Make sure that the ServerRoot directories (especially the log directories and files) are not writable by anyone but the root user. You do not need to give Apache user/group read or write permission in log directories. Enabling anyone other than the root user to write files in the log directory could lead to a major security hole.

# Disabling default access

A strict security model dictates that no default access exists, so get into the habit of permitting no access at first. Permit specific access only to specific locations. To implement no default access, use the following configuration segment in one of your Apache configuration files:

```

<Directory />
    Order deny,allow
    Deny from all
</Directory>

```

This disables all access first. Now, if you need to enable access to a particular directory, use the <Directory> container again to open that directory. For example, if you want to permit access to /www/mysite/public/htdocs, add the following configuration:

```
<Directory "/www/mysite/public/htdocs">
    Order deny,allow
    Allow from all
</Directory>
```

This method—opening only what you need—is a preventive security measure and is highly recommended.