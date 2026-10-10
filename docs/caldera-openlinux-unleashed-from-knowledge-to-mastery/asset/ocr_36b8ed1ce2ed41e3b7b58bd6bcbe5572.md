The most common way to enable SSI is to indicate that files with a certain filename extension (typically .shtml) are to be parsed by the server when they are served. This is accomplished with the following lines in your `srm.conf` file:

```
# To use server-parsed HTML files
# AddType text/html .shtml
# AddHandler server-parsed .shtml
```

By uncommenting the `AddType` and `AddHandler` lines, you could tell the server to parse all `.shtml` files for SSI directives.

The less commonly used way of enabling SSI is with the `XBitHack` directive. `XBitHack` can be set to a value of on, off, or full and can be set in the server config, per `<Directory>`, per `<VirtualHost>` or in .htaccess files. If the `XBitHack` directive is on, it indicates that all files with the user execute bit set should be parsed for SSI directives. This has two main advantages. One is that you do not need to rename a file and change all links to that file simply because you want to add a little dynamic content to it. The other reason is more cosmetic—users looking at your Web content cannot tell by looking at the filename that you are generating a page dynamically—and so your wizardry is just that tiny bit more impressive. If `XBitHack` is set to full, Apache also tests the group execute bit. If it is on, it returns a `Last-Modified` header containing the file's last modified time; otherwise, it doesn't generate a `Last-Modified` header. Allowing a `Last-Modified` header to be generated allows the data to be cached.

In addition to these directives, the `Options Includes` directive must be specified for directories where you want to permit SSI. This may be set in the server `access.conf` file or in an .htaccess file.

# Basic SSI Directives

SSI directives look similar to HTML comment tags. The syntax follows:

```
<!--#element attribute=value attribute=value ... -->
```

The `element` can be one of the following:

`config`		This lets you set various configuration options regarding how the document parsing is handled. Because the page is parsed from top to bottom, `config` directives should appear at the top of the HTML document. Three configurations can be set with this command:

`errormsg`		Allows you to set the error message that is returned to the client if something goes wrong while parsing the document. This is usually [an error occurred while processing this directive], but you can set it to anything with this directive.

```
Example: <!–-#config errormsg='[It's broken, dude]'–>
```