
## 922 CHAPTER 26 APACHE: SETTING UP A WEB SERVER

### UseCanonicalName

Specifies the method the server uses to identify itself.

UseCanonicalName On | Off | DNS

- On: Apache uses the value of the ServerName directive (page 912) as its identity.
- Off: Apache uses the name and port from the incoming request as its identity.
- DNS: Apache performs a DNS reverse name resolution (page 831) on the IP address from the incoming request and uses the result as its identity. Rarely used.

This directive is important when a server has more than one name and needs to perform a redirect. Ubuntu does not set this directive because it does not set the Server-Name directive (page 912). Once you set ServerName, change UseCanonicalName to On. See page 935 for a discussion of redirects and this directive.

Contexts: server config, virtual host, directory

Specify in sites-available/*

Default: Off

Ubuntu: none

## LOGGING DIRECTIVES

### ErrorLog Specifies Apache sends error messages.

```
ErrorLog filename| syslog[facility]
```

where filename specifies the name of the file, relative to ServerRoot (page 926), that Apache sends error messages to. The syslog keyword specifies that Apache send errors to syslog (page 625); facility specifies which syslog facility to use. The default facility is local.

Contexts: server config, virtual host

Specify in httpd.conf or sites-available/*

Default: logs/error_log

Ubuntu: /var/log/apache2/error.log

### LogLevel Specifies the level of error messages that Apache logs.

```
LogLevel level
```

where level specifies that Apache log errors of that level and higher (more urgent). Choose level from the following list, which is presented here in order of decreasing urgency and increasing verbosity:

- - System unusable messages
- Need for immediate action messages
- Critical condition messages
- Error condition messages
- Nonfatal warning messages

## CONFIGURATION DIRECTIVES 923

notice Normal but significant messages
- info Operational messages and recommendations
- debug Messages for finding and solving problems

Contexts: server config, virtual host
Specify in httpd.conf or sites-available/*
Default: warn
Ubuntu: warn

## DIRECTIVES THAT CONTROL CONTENT

### AddHandler Creates a mapping between filename extensions and a builtin Apache handler.

AddHandler handler extension [extension] ...

where handler is the name of a builtin handler and extension is a filename extension that maps to the handler. Handlers are actions that are built into Apache and are directly related to loaded modules. Apache uses a handler when a client requests a file with a specified extension.

For example, the following AddHandler directive causes Apache to process files that have a filename extension .cgi with a cgi-script handler:

```
AddHandler cgi-script .cgi
```

See “Type Maps” on page 935 for another example of an AddHandler directive.

Contexts: server config, virtual host, directory, .htaccess
Specify in httpd.conf
Default: none
Ubuntu: type-map var

### Alias Maps a URI to a directory or file.

Alias pathname where must match part of the URI that the client requested to invoke the alias. The pathname is the absolute pathname of the target of the alias, usually a directory.

For example, the following alias causes Apache to serve /usr/local/pix/milk.jpg when a client requests http://www.example.com/pix/milk.jpg:

```
Alias /usr/local/pix
```

In some cases, you need to use a <Directory> container (page 915) to grant access to aliased content.

Contexts: server config, virtual host
Specify in httpd.conf, sites-available/*, or mods-available/alias.conf
Default: None
Ubuntu: /icons/ /usr/share/apache2/icons/ and /doc/ /usr/share/doc/

## 924 CHAPTER 26 APACHE: SETTING UP A WEB SERVER

### ErrorDocument Specifies the action Apache takes when the specified error occurs.

# ErrorDocument code action

where is the error code (page 948) that this directive defines a response for and action is one of the following:

- string: Defines the message that Apache returns to the client.
- absolute pathname: Points to a local script or other content that Apache redirects the client to.
- URI: Points to an external script or other content that Apache redirects the client to.

When you do not specify this directive for a given error, Apache returns a hardcoded error message when that error occurs.

Some examples of ErrorDocument directives follow:

```
ErrorDocument 403 "Sorry, access is forbidden."
ErrorDocument 403 /cgi-bin/uh-uh.pl
ErrorDocument 403 http://errors.example.com/not_allowed.html
```

Contexts: server config, virtual host, directory, .htaccess
Specify in httpd.conf
Default: none; Apache returns hardcoded error messages
Ubuntu: none (but the comments in apache2.conf)

### IndexOptions Specifies how Apache displays directory listings.

IndexOptions [|option] [[|option]] ...

where option can be any combination of the following:

- DescriptionWidthn=: Sets the width of the description column to n characters. Use * in n to accommodate the widest description.
- FancyIndexing: In directory listings, displays column headers that are links. When you click one of them, Apache sorts the display by the content of the column. Clicking the link second time reverses the order.
- FoldersFirst: Starts the sorting so that directories come before files. Use only with FancyIndexing.
- HTMLTableAsLinks: Makes the icons clickable. Use only with FancyIndexing.
- IconHeightn=: Sets the height of icons to n pixels. Use only with IconWidth.
- IconWidthn=: Sets the width of icons to n pixels. Use only with IconHeight.
- IgnoreCase: Ignores case when sorting names.
- IgnoreClient: Ignores options the client supplied in the URI.
- NameWidth=n: Sets the width of the filename column to n characters. * in place of n to accommodate the widest filename.
- ScanHTMLTitles: Extracts and displays titles from HTML documents. Use only with FancyIndexing. Not normally used because it is CPU and disk intensive.
- SupressColumnSorting: Suppresses clickable column headings that can be used for sorting columns. Use only with FancyIndexing.
- SuppressHTMLPreamble: Suppresses the contents of the file specified by the Header-Name directive, even if it exists.
- SuppressIcon: Suppresses icons. Use only with FancyIndexing.
- SuppressLastModified: Suppresses the modification date. Use only with FancyIndexing.
- SuppressRules: Suppresses horizontal lines. Use only with FancyIndexing.
- SuppressSize: Suppresses file sizes. Use only with FancyIndexing.
- VersionSort: Returns version numbers (in filenames) in a natural way – character strings, except for substrings of digits, are not affected.

As an example, suppose a client requests a URI that points to a directory (such as http://www.example.com/support/) and none of the files specified by the Directory-Index directive (page 914) is present in that directory. If the directory hierarchy is controlled by a .htaccess file and AllowOverride (page 930) is set to allow indexes, then Apache displays a directory listing according to the options specified by this directive.

When this directive appears more than once in a directory, Apache merges the options from the directives. Use + and – merge IndexOptions options with options from higher-level directories. (Unless use + or with all options, Apache discards any option set in higher-level directories.) For the following directives and containers set the options for /custsup/download to Version-Sort; Apache discards FancyIndexing and IgnoreCase in the download directory because there is no + or before VersionSort in the second <Directory> container:

```
<Directory /custsup
  IndexOptions FancyIndexing
  IndexOptions IgnoreCase
</Directory>
```

```
<Directory /custsup/download
  IndexOptions VersionSort
</Directory>
```

## 926 CHAPTER 26 APACHE: SETTING UP A WEB SERVER

```
<Directory /custsup>
  IndexOptions FancyIndexing
  IndexOptions IgnoreCase
</Directory>
```

```
<Directory /custsup/download>
  IndexOptions +VersionSort
</Directory>
```

Contexts: server config, virtual host, directory, .htaccess

Specify in httpd.conf
Default: none; lists filenames

Ubuntu FancyIndexing VersionSort HTMLTable NameWidth=* Charset=UTF-8

### ServerRoot Specifies the root directory for server files (not content).

ServerRoot directory
where directory specifies the pathname of the root directory for the files that make the server. Apache appends directory to relative paths in httpd.conf. This directive does not specify the location of the content that Apache serves; the DocumentRoot directive performs that function. Do not change this value unless you move the server files.

Contexts: server config
Specify in httpd.conf
Default: /usr/local/apache
Ubuntu: /etc/apache2

### ServerTokens Specifies the server information that Apache returns to a client.

ServerTokens Prod | Major | Minor | OS | Full
- Prod: Returns the product name: Apache. Also ProductOnly.
- Major: Returns the major release number of the server: Apache/2.
- Minor: Returns the major and minor release numbers of the server: Apache/2.2.
- Min: Returns the complete version: Apache/2.2.4. Also Minimal.
- OS: Returns the name of the operating system and the complete version: Apache/2.2.4 (Ubuntu). Provides less information that might help a malicious user than Full does.
- Full: Same as OS, except Full also sends the names and versions of non-ASF modules: Apache/2.2.4 (Ubuntu) PHP/5.1.2.

Unless you clients to know the details of the software you are running, ServerTokens to reveal as little as possible.

Contexts: server config
Specify in httpd.conf
Default: Full
Ubuntu: Full
