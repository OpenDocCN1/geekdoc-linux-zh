
*All*: Denies content to all clients.

*host*: Denies content to the client(s) specified by *host*, which can take several forms: *host* can be an FQDN, a partial domain name (such as `example.com`), an IP address, a partial IP address, or a network/netmask pair.

*var*: Denies content when the environment variable named *var* is set. You can set a variable with the SetEnvIf directive.

-   Contexts: `directory`, `.htaccess`
-   Default: none
-   Fedora/RHEL: none

*Order* Specifies default access and the order in which Allow and Deny directives are evaluated.

```
Order Deny,Allow | Allow,Deny
```

**Deny,Allow**: Allows access by default; denies access only to clients specified in Deny directives. (First evaluates Deny directives, then evaluates Allow directives.)

**Allow,Deny**: Denies access by default; allows access only to clients specified in Allow directives. (First evaluates Allow directives, then evaluates Deny directives.)

Access granted or denied by this directive applies to the directory hierarchy specified by the container or `.htaccess` file this directive appears in.

There must not be SPACES on either side of the comma. Although Fedora/RHEL has a default of Allow,Deny, which denies access to all clients not specified by Allow directives, the next directive in `httpd.conf`, `Allow from all`, grants access to all clients:

```
Order allow,deny
Allow from all
```

You can restrict access by specifying Deny,Allow to deny all access and then specifying only those clients you want to grant access to in an Allow directive. The following directives grant access to clients from the `example.net` domain only and would typically appear within a `<Directory>` container (page 855):

```
Order deny,allow
Deny from all
Allow from .example.net
```

-   Contexts: `directory`, `.htaccess`
-   Default: Deny,Allow
-   Fedora/RHEL: Allow,Deny

## THE FEDORA/RHEL httpd.conf FILE

This section highlights some of the important features of the Fedora/RHEL `httpd.conf` file, which is based on the `httpd.conf` file distributed by Apache. This heavily commented file is broken into the following parts (as is this section):

-   1. Global Environment—Controls the overall functioning of the Apache server.
-   2. Main Server Configuration—Configures the default server (as opposed to virtual hosts) and provides default configuration information for virtual hosts.
-   3. Virtual Hosts—Configures virtual hosts. For more information refer to “Virtual Hosts” on page 874.

### SECTION 1: GLOBAL ENVIRONMENT

**ServerTokens** The ServerTokens directive (page 865) is set to OS, which causes Apache, when queried, to return the name of the operating system and the complete version number of Apache:

```
ServerTokens OS
```

**ServerRoot** The ServerRoot directive (page 865) is set to /etc/httpd, which is the pathname that Apache prepends to relative pathnames in httpd.conf.

```
ServerRoot "/etc/httpd"
```

**<IfModule Multiprocessing modules (MPMs) allow you to change the way Apache works by changing the modules it uses. The <IfModule> containers (page 856) allow you to use the same httpd.conf file with different modules. The directives in an <IfModule> container are executed only if the specified module is loaded.

The section of httpd.conf that starts with the comment

```
# Server-Pool Size Regulation (MPM specific)
```

holds two `<IfModule>` containers (page 856) that configure Apache, depending on which module, prefork or worker, is loaded. Fedora/RHEL ships Apache with the prefork module loaded; this section does not discuss the `<IfModule>` container for the worker module. (See the comments in the /etc/sysconfig/httpd file if you want to load the worker module.)

The prefork `<IfModule>` container, shown below, holds directives that control the functioning of Apache when it starts and as it runs:

```
<IfModule prefork.c>
StartServers      8
MinSpareServers   5
MaxSpareServers   20
ServerLimit       256
MaxClients        256
MaxRequestsPerChild 4000
</IfModule>
```

**Listen** FEDORA The Listen directive (page 851) does not specify an IP address.

RHEL The Listen directive specifies an IP address of 0.0.0.0, which is the same as not specifying an IP address, so Apache listens on all network interfaces.

```
Listen 80
```

| Directive | Description |
| :--- | :--- |
| LoadModule | There are quite a few LoadModule directives (page 867); these directives load the Apache DSO modules (page 876). |
| Include | The Include directive (page 866) includes the files that match `*.conf` in the /etc/httpd/conf.d directory, as though they were part of httpd.conf: <br> `include conf.d/*.conf` |
| Fedora/RHEL test page | When you first install Apache, there is no index.html file in /var/www/html; when you point a browser at the local Web server, Apache generates error 403, which returns the Fedora/RHEL test page. The mechanism by which this page is returned is convoluted: The Fedora/RHEL httpd.conf file holds an Include directive that includes all files in the conf.d directory that are in the ServerRoot directory (page 865). The welcome.conf file in this directory contains an ErrorDocument 403 directive (page 863) that redirects users who receive this error to error/noindex.html in the DocumentRoot directory (page 852). The noindex.html file is the Fedora/RHEL test page that confirms the server is working but there is no content to display. |

### SECTION 2: MAIN SERVER CONFIGURATION

| Directive | Description |
| :--- | :--- |
| ServerAdmin, ServerName | As Fedora/RHEL is shipped, the ServerAdmin and ServerName directives are commented out. Change them to useful values as suggested in the ServerAdmin (page 851) and ServerName (page 852) sections. |
| DocumentRoot | The DocumentRoot directive (page 852) appears as follows: <br> `DocumentRoot "/var/www/html"` <br> You need to modify this directive only if you want to put your content somewhere other than /var/www/html. |
| <Directory> | The following `<Directory>` container (page 855) sets up a restrictive environment for the entire local filesystem (specified by /): <br> `<Directory /> Options FollowSymLinks AllowOverride None </Directory>` <br> The Options directive (page 867) allows Apache to follow symbolic links but disallows many options. The AllowOverride directive (page 869) causes Apache to ignore .htaccess files. You must explicitly enable less restrictive options if you want them, but be aware that doing so can expose the root filesystem and compromise system security. <br> Next another `<Directory>` container sets up less restrictive options for the DocumentRoot (/var/www/html). The code in httpd.conf is interspersed with many comments. Without the comments it looks like this: <br> `<Directory "/var/www/html"> Options Indexes FollowSymLinks AllowOverride None Order allow,deny Allow from all </Directory>` |

The `Indexes` option in the `Options` directive allows Apache to display directory listings. The `Order` (page 870) and `Allow` (page 868) directives combine to allow requests from all clients. This container is slightly less restrictive than the preceding one, although it still does not allow Apache to follow directives in `.htaccess` files.

**DirectoryIndex**
As explained on page 853, the `DirectoryIndex` directive causes Apache to return the file named `index.php`, `index.html`, `index.htm`, or `index.shtml` from a requested directory. Because `Options Indexes` is specified in the preceding `<Directory>` container, if none of these files exists in a queried directory, Apache returns a directory listing:

```
DirectoryIndex index.html index.html.var
```

There are many more directives in this part of the `httpd.conf` file. The comments in the file provide a guide as to what they do. There is nothing here you need to change as you get started using Apache.

### SECTION 3: VIRTUAL HOSTS

All lines in this section are comments or commented-out directives. If you want to set up virtual hosts, see page 874.

### REDIRECTS

Apache can respond to a request for a URL by asking the client to request a different URL. This response is called a *redirect*. A redirect works because redirection is part of the HTTP implementation: Apache sends the appropriate response code and the new URL, and a compliant browser requests the new location.

The `Redirect` directive can establish an explicit redirect that sends a client to a different page when a Web site is moved. Or, when a user enters the URI of a directory in a browser but leaves off the trailing slash, Apache can automatically redirect the client to the same URI terminated with a slash.

**UseCanonicalName**
The `ServerName` directive (page 852), which establishes the name of the server, and the `UseCanonicalName` directive (page 861) are both important when a server has more than one name and needs to perform an automatic redirect. For example, assume the server with the name `zach.example.com` and the alias `www.example.com` has `ServerName` set to `www.example.com`. When a client specifies a URI of a directory but leaves off the trailing slash (`zach.example.com/dir/`), Apache has to perform a redirect to determine the URI of the requested directory. When `UseCanonicalName` is set to `On`, Apache uses the value of `ServerName` and returns `www.example.com/dir/`. With `UseCanonicalName` set to `Off`, Apache uses the name from the incoming request and returns `zach.example.com/dir/`.
