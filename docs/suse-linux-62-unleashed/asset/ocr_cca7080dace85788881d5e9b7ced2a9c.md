# Networking and Internet Services
PART II

For example, you will see the following in your httpd.conf file:

```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

# Options Directives

Options can be None, All, or any combination of Indexes, Includes, FollowSymLinks, ExecCGI, or MultiViews. MultiViews is not included in All and must be specified explicitly. These options are explained in the following table.

+   - None None of the available options are enabled for this directory.