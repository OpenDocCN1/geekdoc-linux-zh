# Table 21-1: Apache Modules Loaded in Ubuntu Server

| Module | Description |
|---|---|
| alias | Maps directory paths on the server to the web server document tree |
| auth_basic | Provides basic user authentication by looking up user accounts in a specific provider |
| authn_file | Restricts access based on a user account defined in a text file |
| authz_default | Rejects user access if no authentication is used (default module) |
| authz_groupfile | Restricts access based on groups defined in a text file |
| authz_host | Restricts access based on hostnames or IP addresses |
| authz_user | Restricts access to specific pages using user accounts |
| autoindex | Creates automatic directory listings |
| cgi | Executes common gateway interface (CGI) scripts from web pages |
| dir | Handles basic filesystem directories |
| env | Passes system environment variables to CGI scripts |
| mime | Determines file types using file extensions for handling files |
| negotiation | Selects a document type that matches the client's capabilities |
| php5 | The PHP version 5 preprocessor |
| setenvif | Sets environment variables based on client information |
| status | Displays the server status using a specially formatted web page |

Use the apt-get program (see Chapter 13, "Software Installs and Updates") from the command line to install additional modules directly from the Ubuntu server software repositories. To download a new module, use this command:

```
sudo apt-get install modname
```

This command downloads the module from the Ubuntu server repository into a special folder located at /etc/apache2/mods-available. To enable the module, you need to perform one more command:

```
a2enmod modname
```

This command makes the module active in the Apache web server.

Secret
To remove an active module from the configuration, don't delete the configuration files. Instead, use this command:

```
a2dismod modname
```

This command removes the module from the configuration files but keeps it in the mods-available folder for future use, if required.