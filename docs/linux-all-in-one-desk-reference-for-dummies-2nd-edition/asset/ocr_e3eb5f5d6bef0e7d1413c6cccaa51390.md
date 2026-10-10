+   ♦ `MaxClients num`: Sets the limit on the number of clients that can simultaneously connect to the server. The default value is 150. The value of `MaxClients` cannot be more than 256.

+   ♦ `LoadModule module modules/modfile.so`: Loads a module that was built as a Dynamic Shared Object (DSO). You have to specify the module name and the module’s object file. Because the order in which modules load is important, leave these directives as they appear in the default configuration file. *Note:* The `mod_ssl` module provides support for encryption using the Secure Sockets Layer (SSL) protocol.

# Resource configuration directives

The resource configuration directives specify the location of the Web pages, as well as how to specify the data types of various files. To get started, you can leave the directives at their default settings. These are some of the resource configuration directives for the Apache Web server:

+   ♦ `DocumentRoot pathname`: Specifies the directory where the HTTP server finds the Web pages. In Debian, the default `DocumentRoot` is `/var/www/apache2-default`. In Fedora Core, `DocumentRoot` is `/var/www/html`. In SUSE, `DocumentRoot` is `/srv/www/htdocs`. In Knoppix and Xandros, `DocumentRoot` is `/var/www`. If you place your HTML documents in another directory, set `DocumentRoot` to that directory.

+   ♦ `UserDir dirname`: Specifies the subdirectory below a user’s home directory where the HTTP server looks for Web pages when a username appears in the URL (in an URL such as `http://www.xyz.net/~naba`, for example, which includes a username with a tilde prefix). By default, the `UserDir` feature is turned off by setting `dirname` to disable. If you want it enabled, you can set it to `public_html`, which means that a user’s Web pages are in the `public_html` subdirectory of that user’s home directory. `UserDir` is disabled by default because it can open up the file system to the world. Apache documentation recommends adding the following line to the `httpd.conf` file:
+   
+       `UserDir disabled root`

+   ♦ `DirectoryIndex filename filename2 ...`: Indicates the server return default file or files when the client does not specify a document. The default `DirectoryIndex` is `index.html`. If the Apache Web server does not find this file, it returns an index (basically, a nice-looking listing of the files) of that directory, provided indexing is allowed for that directory.