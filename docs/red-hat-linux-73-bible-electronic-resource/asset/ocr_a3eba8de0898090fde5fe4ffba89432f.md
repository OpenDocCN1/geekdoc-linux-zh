# ## Allowing password updates

The following lines allow the `http_put` feature to be used to generate new passwords. As noted in the comment, this feature allows an application, such as the Netscape Gold, to use its publish feature to change user-authentication information for HTTP users.

```
"#\n# Allow `http_put` (such as Netscape Gold's `publish` feature)\n# Use `httpasswd` to generate `/etc/httpd/conf/passwd`.\n#\n#<IfModule `mod_put.c>`\n#\tAlias `/upload` `/tmp`\n#\t<Directory `/tmp>`\n#\t\t`EnablePut On`\n#\t\t`AuthType Basic`\n#\t\t`AuthName Temporary`\n#\t\t`AuthUserFile /etc/httpd/conf/passwd`\n#\t\t`EnableDelete Off`\n#\t\t`umask 007`\n#\t\t<Limit `PUT>`\n#\t\t\trequire valid-user\n#\t\t</Limit>\n#\t</Directory>\n#</IfModule>"
```

> **NOTE:** If you are following along in the `httpd.conf` file, you notice that we are skipping descriptions of the server-status lines and server-info lines. Those features are described later in the "Monitoring Server Activities" section.

# ## Allowing access to local documentation

Documentation that comes with each software package installed with Red Hat Linux is stored in the `/usr/share/doc` directory. The following lines make that directory available to users on your local computer through the `httpd` service (i.e., from their Web browsers):

```
"# Allow access to local system documentation from localhost\n`Alias /doc/ /usr/share/doc/`\n`<Directory /usr/share/doc>`\n	`order deny,allow`\n	`deny from all`\n	`allow from localhost .localdomain`\n	`Options Indexes FollowSymlinks`\n`</Directory>`"
```

# ## Enabling proxy and caching services

Proxy and caching services are turned off by default. You can turn them on by uncommenting several values, presented below: