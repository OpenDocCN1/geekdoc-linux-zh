
## Apache Configuration Files

The Apache web server requires a few configuration files to operate. When you select to install the LAMP server from the Ubuntu server installation menu, the installation process installs the Apache web server package, including preconfigured Apache files, to create a basic web server environment.

All of the Apache web server configuration files are located in the `/etc/apache2` folder. They include the following files and folders:

- `apache2.conf`: the main Apache web server configuration file that the Apache web server reads
- `conf.d`: a folder containing files that have specific configuration features included in the Apache configuration (by default, Ubuntu creates configuration options to define the character set of the server and set the security level of the server)
- `envvars`: a configuration file to set specific environment variables for the Apache web server
- `httpd.conf`: a configuration file for adding local configuration customizations
- `mods-available`: a folder that contains the configuration settings for modules available for the server
- `mods-enabled`: a folder containing links to the enabled configuration settings stored in the mods-available folder
- `ports.conf`: a configuration file that specifies which TCP ports the Apache web server should listen on
- `sites-available`: a folder containing available site definitions for virtual hosts
- `sites-enabled`: a folder containing links to the active site definition files in the sites-available folder

The `/etc/apache2/apache2.conf` file is the main configuration file that the Apache web server processes. This file references the individual configuration files for specific configuration features, such as the TCP ports used and the virtual hosts to create.

## Apache Modules

The core Apache2 program supports only basic web page hosting features. Any other functionality needed for the web server (including sending PHP files to the PHP preprocessor) requires a plug-in module. Modules provide a host of various additional features to the Apache web server, including the capability to process PHP files.

Ubuntu stores modules in the `/etc/apache2/mods-available` folder. You can look in that folder to see what modules are installed by default in the Ubuntu server.

However, there’s a subtle difference in what the Ubuntu server does when handling Apache modules. Although modules are stored in the `/etc/apache2/mods-available` folder, those modules aren’t necessarily active in the Apache web server configuration.

For a module to become active, Ubuntu creates a file link in the `/etc/apache2/mods-enabled` folder that points to the module files in the `mods-available` folder. The Ubuntu server enables a few modules by default, providing for a robust web server environment. The modules enabled by default in the Ubuntu server are shown in Table 21-1.

### Table 21-1: Apache Modules Loaded in Ubuntu Server

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
