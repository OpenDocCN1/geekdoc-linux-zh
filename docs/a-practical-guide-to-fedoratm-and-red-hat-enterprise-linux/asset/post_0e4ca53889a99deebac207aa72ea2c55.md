
**Denies content when the environment variable named `var` is set. You can set a variable using the `SetEnvIf` directive.**

- Contexts: directory, .htaccess
- Default: none
- Fedora/RHEL: none

### Order
*Specifies the default access and the order in which `Allow` and `Deny` directives are evaluated.*

```
Order Deny,Allow | Allow,Deny
```

**Deny,Allow**—Allows access by default; denies access only to clients specified in `Deny` directives (first evaluates `Deny` directives and then evaluates `Allow` directives).

**Allow,Deny**—Denies access by default; allows access only to clients specified in `Allow` directives (first evaluates `Allow` directives and then evaluates `Deny` directives). There must not be a SPACE on either side of the comma. Access defaults to the second entry in the pair (`Deny,Allow` defaults to `Allow`) if there is no `Allow from` or `Deny from` directive that matches the client. If a single `Allow from` or `Deny from` directive matches the client, that directive overrides the default. If multiple `Allow from` and `Deny from` directives match the client, Apache evaluates the directives in the order specified by the `Order` directive; the last match takes precedence.

Access granted or denied by this directive applies to the directory hierarchy specified by the container or `.htaccess` file this directive appears in. In the next directive, `Allow from all` grants access to all clients:

```
Order allow,deny
Allow from all
```

You can restrict access by specifying `Deny,Allow` to deny all access and then specifying only those clients you want to grant access to in an `Allow` directive. The following directives grant access to clients from the **example.net** domain only and would typically appear within a `<Directory>` container (page 945):

```
Order deny,allow
Deny from all
Allow from .example.net
```

- Contexts: directory, .htaccess
- Default: Deny,Allow

### Require
*Tests/specifics whether a user is authorized to access a directory hierarchy.*

`Require` `all granted` | `all denied` | `ip addr`

where `addr` is one or more SPACE-separated IP addresses of systems that are allowed to access the directory hierarchy.

- **all granted**: Any user can access the directory hierarchy.
- **all denied**: No user can access the directory hierarchy.

The **httpd.conf** file contains several `Require` directives. The first, because it is in a `<Directory>` container that specifies the root directory, denies access to the entire file system:

```
<Directory />
AllowOverride none
Require all denied
</Directory>
```

However, that restriction is immediately relaxed for the **www** child directory.

```
<Directory "/var/www/">
AllowOverride None
Require all granted
</Directory>
```

- Context: directory, .htaccess
- Default: none

## ADVANCED CONFIGURATION

This section describes how to configure some advanced features of Apache.

### REDIRECTS

Apache can respond to a request for a URI by asking the client to request a different URI. This response is called a *redirect*. A redirect works because redirection is part of the HTTP implementation: Apache sends the appropriate response code and the new URI, and a compliant browser requests the new location.

The `Redirect` directive can establish an explicit redirect that sends a client to a different page when a Web site is moved. Or, when a user enters the URI of a directory in a browser but leaves off the trailing slash, Apache can automatically redirect the client to the same URI terminated with a slash.

The `ServerName` directive (page 942), which establishes the name of the server, and the `UseCanonicalName` directive (page 951) are both important when a server has more than one name and needs to perform an automatic redirect. For example, assume the server with the name *zach.example.com* and the alias **www.example.com** has `ServerName` set to **www.example.com**. When a client specifies a URI of a directory but leaves off the trailing slash (*zach.example.com/dir/*), Apache has to perform a redirect to determine the URI of the requested directory. When `UseCanonicalName` is set to `On`, Apache uses the value of `ServerName` and returns **www.example.com/dir/**. With `UseCanonicalName` set to `Off`, Apache uses the name from the incoming request and returns *zach.example.com/dir/*.

### CONTENT NEGOTIATION

Apache can serve multiple versions of the same page, using a client's preference to determine which version to send. The process Apache uses to determine which version of a page (file) to send is called content negotiation. Apache supports two methods of content negotiation: type maps and `MultiViews` search, which can work together.

#### TYPE MAPS

The following `AddHandler` directive from `httpd.conf` would tell Apache to use any filename ending in `.var` as a type map (if it were not commented out):

```
# AddHandler type-map var
```

To see how type maps work, create the following files in `/var/www/html`:

```
$ cat /var/www/html/index.html.en
<html><body><h1>Hello</h1></body></html>
```

```
$ cat /var/www/html/index.html.fr
<html><body><h1>Bonjour</h1></body></html>
```

```
$ cat /var/www/html/index.html.var
URI: index.html.en
Content-Language: en
Content-Type: text/html; charset=ISO-8859-1

URI: index.html.fr
Content-Language: fr
Content-Type: text/html; charset=ISO-8859-1
```

If your browser's preferred language is set to English (en), it will display the Hello page when you browse to `http://localhost/index.html.var`. If your browser's preferred language is set to French (fr), it will display the Bonjour page. (With the `MultiViews` option turned on, as it is by default, the browser displays the correct page when you browse to `http://localhost`. See the next section.) You can change the default language in Firefox by selecting EditPreferences from the menubar, clicking the Content icon, and finally clicking Choose from the Languages frame. Select a language from the "Select a language to add" combo box, if necessary, and then move the preferred language to the top of the list. In the example, the charset assignments are not necessary. However, they would be helpful if you were sending pages using different encodings such as English, Russian, and Korean.

Type maps are used for more than selecting among different languages. Instead of matching `Content-Language` as in the preceding example, the map could match `Content-type` and send jpeg or png images depending on how the browser's preferences are set.

#### MultiViews

When you set the `MultiViews` option on a directory, Apache attempts to deliver the correct page when a requested resource does not exist. In `httpd.conf`, add `MultiViews` to the `Options` line in the `<Directory>` container as follows:

```
<Directory "/var/www/html">
    ...
    Options Indexes FollowSymlinks MultiViews
    ...
```

![](img/243613168ac865b539f12460d966088e_1020_0.png)

**Figure 26-1** A server-generated directory listing

To see how `MultiViews` work, remove the `/var/www/html/index.html` and type map file you created in the preceding section. Now browse to `http://localhost`. The proper language page is displayed, but why?

When a browser sends Apache a request for a directory, Apache looks for a file named `index.html` in that directory. In the example, Apache does not find the file. If `MultiViews` is enabled, Apache looks for files named `index.html.*`. In the example it finds `index.html.en` and `index.html.fr`. Apache effectively creates a type map on the fly, mapping the `index.html.*` files to various languages, and sends its best guess as to the page you want.

#### Which to use: MultiViews or type maps?

**caution** `MultiViews` provides an easy way to serve multiple versions of the same file without having to create a type map. However, `MultiViews` is slower than type maps. Also, if you require finer-grained control over which version of a resource should be sent, type maps are a better solution.

### SERVER-GENERATED DIRECTORY LISTINGS (INDEXING)

When a client requests a directory, the Apache configuration determines what is returned to the client. Apache can return a file as specified by the `DirectoryIndex` directive
