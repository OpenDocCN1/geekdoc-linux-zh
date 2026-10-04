
# Configuring the Apache Server

- PidFile filename: Sets the file where HTTPD stores its process ID.
The default PidFile is /var/run/httpd.pid. You can use this information to kill or restart the HTTP daemon. The following example shows how to restart httpd:

```
kill -HUP 'cat /var/run/httpd.pid'
```

- MaxClients num: Sets the limit on the number of clients that can simultaneously connect to the server. The default value is 150. The value of MaxClients cannot be more than 256.

- LoadModule modules/mod_file: Loads a module as a Dynamic Shared Object (DSO). You have to specify the module name and the module's object file. Because the order in which modules are loaded is important, leave these directives as they appear in the default configuration file. Note: The mod_ssl module provides support for encryption using the Secure Sockets Layer (SSL) protocol.

# Resource configuration directives

The resource configuration directives specify the location of the Web pages, as well as how to specify the data types of various files. To get started, you can leave the directives at their default settings. These are some of the resource configuration directives for the Apache web server:

- DocumentRoot pathname: Specifies the directory where the HTTP server finds the Web pages. In Fedora Core, the place your HTML documents is in /var/www/html. If you place your HTML documents in another directory, set DocumentRoot to that directory.

- UserDir dirname: Specifies the subdirectory below a user's home directory where the HTTP server looks for Web pages when a username appears in the URL (in an URL as http://www.psn.net/-name, for example, which includes a username with a tilde prefix). By default, the UserDir feature is turned off by setting dirname to disable. If enabled, you can set it to public_html, which means that a user's pages are in the public_html subdirectory of their home directory.

- DirectoryIndex filename filename2 ...: Indicates the server return file or files when the client does not specify a document. The default DirectoryIndex is index.html. If httpd does not find this file, it returns an index (basically, a nice-looking list of the files) of that directory, provided indexing is allowed for directory.

- AccessFileName filename: Specifies the name of the file that may appear in each directory that contains documents and indicates who has permission to access the contents of that directory. The default AccessFileName is .htaccess. The syntax of this file is the same as that of Apache access-control directives, which I discuss in the next section.

![](img/d9230b719dc0efd80851f363d8c6f571_653_0.png)

# Configuring the Apache Web Server

- AddType type/subtype extension: Associates a file extension with a MIME data type (of the form type/subtype, such as text/plain or image/gif). Thus, to have the server treat files with the .lst extension as plain-text files, specify the following:

```
AddType text/plain .lst
```

The default MIME types and extensions are listed in the /etc/mime.types.

- AddEncoding type extension: Associates an encoding with a file extension. To have the server mark files with .gz or .tgz as encoded with the x-gzip encoding method (the standard name for the GZIP encoding), specify the following:

```
AddEncoding x-gzip gz tgz
```

- DefaultType type/subtype: Specifies the MIME type that the server uses if it cannot determine the type from the file extension. DefaultType assumes the MIME type to be text/html. In the default httpd.conf file, DefaultType is specified as text/plain.

- Redirect requested-file actual-URL: Specifies that any requests for requested-file be redirected to actual-URL.

- Alias requested-dir actual-dir: Specifies that the server uses actual-dir to locate files in the requested-dir directory (in other words, requested-dir is an alias for actual-dir). To have requests for the /icons directory to /var/www/icons, specify the following:

```
Alias /icons /var/www/icons/
```

- ScriptAlias requested-dir actual-dir: Specifies the real name of the directory where scripts for the Common Gateway Interface (CGI) are located. The default configuration file contains this:

```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```

This directive means that when a web browser requests a script, such as cgi-bin-cgi, the HTTP server runs the script at /var/www/cgi-bin-cgi.

- DefaultIcon iconfile: Specifies the location of the default icon that the server uses for files that have no icon information. By default, DefaultIcon is /icons/unknown.gif.

- ReadmeName filename: Specifies the name of a README file whose contents are added to the end of an automatically generated directory listing. The default ReadmeName is README.

- HeaderName filename: Specifies the name of a header file whose contents are prepended to an automatically generated directory listing.

- AddDescription "file description" filename: Specifies that the file description string display next to the specified filename in the directory listing. You can use a wildcard, as *.html, as the filename. For example, the following directive describes files ending with .tgz GZIP compressed tar archives:

```
AddDescription "GZIP compressed tar archive" .tgz
```

- AddIcon iconfile extension1 extension2 ... : Associates an icon with one or more file extensions. The following directive associate the icon /icons/text.gif with the file extension .txt:

```
AddIcon /icons/text.gif .txt
```

- AddByType MIME types: Associates an icon with a group of file types as a wildcard form of MIME types (such as /* or *). To associate an icon file of /icons/text.gif with all text types, specify the following:

```
AddByType (TXT, /icons/text.gif) */*
```

This directive tells the server to use TXT in place of the icon for clients that cannot accept images. (Browsers tell the server what types of data they can accept.)

- AddByEncoding encoding1 encoding2 ... : Specifies an icon for one or more encoding types (such as x-compress or x-zip).

- IndexIgnore filename1 filename2 ... : Instructs the server to ignore the specified filenames (typically contain wildcards) when preparing a directory listing. To leave out README, HEADER, and all files with names with a period (.), a trailing tie (-), or a hash mark (#), specify the following:

```
IndexIgnore ??* ~ # HEADER* RCS CVS *v *t
```

- IndexOptions option1 option2 ... : Indicates the options you want in the directory listing prepared by the server. Options can include one or more of the following:

- FancyIcon turns on the fancy directory listing that includes filenames and icons representing the files' sizes, types, and last-modified dates.

- IconHeight=N specifies that icons are N pixels tall.

- IconWidth=N specifies that icons are N pixels wide.

- NameWidth=N makes the filename column N characters wide.

- IconsAreLinks makes the icons act like links.

- ScanHTMLTitles shows a description of HTML files.

| Book VIII |
| Chapter 2 |
| Running the Apache Web Server |

# 630 Configuring the Apache HTML Server

- SuppressHTMLPreamble does not add a standard HTML preamble to the header file (specified by the HeaderName directive).

- SuppressModified stops display of the last date of modification.

- SuppressSize stops display of the file size.

- SuppressDescription stops display of any file description.

- SuppressColumnSorting stops the column headings being links that sort the columns.

ErrorDocument error filename specifies a file the server sends when an error of specific type occurs. You can also provide a text message for an error. Here are some examples:

```
ErrorDocument 403 "no access to this directory"
ErrorDocument 403 /error/noindex.html
ErrorDocument 404 /cgi-bin/bad_link.pl
ErrorDocument 401 /new_subscriber.html
```

If you don't have the ErrorDocument directive, the server sends a builtin error message. The error can be one of the following HTTP/1.1 error conditions (see RFC 2616 at www.ietf.org/rfc/rfc2616.txt or www.faqs.org/rfcs/rfc2616.html for more information):

- 400: Bad Request
- 401: Unauthorized
- 402: Payment Required
- 403: Forbidden
- 404: Not Found
- 405: Method Not Allowed
- 406: Not Acceptable
- 407: Proxy Authentication Required
- 408: Request Timeout
- 409: Conflict
- 410: Gone
- 411: Length Required
- 412: Precondition Failed
- 413: Request Entity Too Large
- 414: Request-URI Too Long
