
```text
AddModule mod_actions.c
AddModule mod_userdir.c
AddModule mod_proxy.c
AddModule mod_alias.c
AddModule mod_rewrite.c
AddModule mod_access.c
AddModule mod_auth.c
AddModule mod_auth_anon.c
AddModule mod_auth_db.c
AddModule mod_digest.c
AddModule mod_expires.c
AddModule mod_headers.c
AddModule mod_usertrack.c
AddModule mod_so.c
AddModule mod_setenvif.c
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
LogFormat "%h %l %u %t \"%r\" %>s %b" common
LogFormat "%{Referer}i -> %U" referer
LogFormat "%{User-agent}i" agent
CustomLog /usr/local/apache/logs/access_log common
PidFile /var/run/httpd.pid
UseCanonicalName on
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
MinSpareServers 8
MaxSpareServers 20
StartServers 10
MaxClients 150
MaxRequestsPerChild 100
```

> **Note**
> 
> The httpd.conf file normally contains substantial comments that describe entries and their purposes. These have been removed for brevity and clarity of presentation in this book. Comments start with the hash mark (#) and continue to the end of the line, as is typical of most Linux configuration files.

> **Note**
> 
> Where the complete absolute path of a file is not specified (such as in the LoadModule directives), the specified path of the file is relative to the directory specified with the ServerRoot directive. Therefore, the file modules/mod_env.so is actually /usr/local/apache/modules/mod_env.so, as in this example.

## The `srm.conf` File

The `srm.conf` file is typically used to specify configuration information related to resources being served by the Apache Web server. For instance, the document root directory for your Web server, supported languages, and directory aliases are defined in this file. The `srm.conf` file is normally located in the default Apache configuration directory (`/usr/local/apache/conf/srm.conf` if Apache is installed from the source code distribution using default settings).

> **Note**
> 
> As mentioned earlier, the configuration directives listed here can also be placed in the `httpd.conf` file. Apache recommends placing the directives in `httpd.conf` but both approaches can be used.

As normally used, this configuration file defines the core parameters that define the operation of the Apache server. This file consists of a series of directives of the general form:

`<Directive Name> <Directive Value>`

A typical `srm.conf` file will likely contain the directives outlined in Table 23.2.

**TABLE 23.2  TYPICAL `srm.conf` DIRECTIVES**

| Directive Name | Description |
|---|---|
| `AccessFileName` | Specifies the name of the access control file. An access control file of the specified name can be placed in a directory in your server’s document tree to specify server-specific access control settings overriding general settings defined in the `access.conf` file. Normally this file is called `.htaccess` and this is the default value of the AccessFileName directive. Because this is a commonly known filename, you can enhance the security of your system by changing the filename for your Web server. The filename should always start with a dot so that it is hidden from directory listings; otherwise, the purposes of changing the filename (to make it harder for attackers to guess the name and download the file for viewing and analysis) are defeated. |
| `AddEncoding` | Specifies a MIME encoding for files with a particular filename extension. Multiple AddEncoding directives normally appear in the `srm.conf` file and the default file contains a pre-defined set of encodings to which you can add your own entries. |
| `AddHandler` | Specifies an application handler for files with a given filename extension. The value of this directive takes the form `<Handler name> <File name extension>`. |
| `AddIcon` | Specifies the icon to display in directory listings for files with a specific filename extension when FancyIndexing is enabled. The value of this directive takes the form `<Icon file name> <File name extension>`. The icon filename should be a path from the root of your Web site. That is, if you access the file as `http://my.host/icons/file.gif` then you want to specify `/icons/file.gif` as the filename. The filename extension should contain the leading dot as in `.txt`. The default `srm.conf` contains a set of icon definitions to which you can add your own AddIcon directives as needed. |
| `AddIconByEncoding` | Specifies the icon to display in directory listings for files of a specific MIME encoding when FancyIndexing is enabled. The MIME encoding must be defined with an AddEncoding directive. The value of this directive takes the form `<Text name>,<Icon file name> <MIME Encoding>`. The icon filename should be a path from the root of your Web site. That is, if you would access the file as `http://my.host/icons/file.gif` then specify `/icons/file.gif` as the filename. The text name is the text to display in place of an icon in text-only browsers. The MIME encoding should be specified with a MIME encoding specified in an AddEncoding directive. The default `srm.conf` contains a set of icon definitions to which you can add your own AddIconByEncoding directives as needed. |
| `AddIconByType` | Specifies the icon to display in directory listings for files of a specific MIME type when FancyIndexing is enabled. The MIME encoding must have been defined with an AddEncoding directive. The value of this directive takes the form `<Text name>,<Icon file name> <MIME type>`. The icon filename should be a path from the root of your Web site. That is, if you would access the file as `http://my.host/icons/file.gif` then specify `/icons/file.gif` as the filename. The text name is the text to display in place of an icon in text-only browsers. The MIME type should be a standardized MIME type as `text/html` or a broad grouping of MIME types specified with a wildcard such as `image/*`. The default `srm.conf` contains a set of icon definitions to which you can add your own AddIconByType directives as needed. |
| `AddLanguage` | Specifies language-specific MIME encodings to be associated with specific filename extensions. The value of this directive takes the form `<MIME language> <Filename extension>`. The MIME language is a two-letter MIME language code such as `en` for English or `de` for German. The filename extension specifies the extension of files in the given language; the extension should include the leading dot as in `.en`. The default `srm.conf` file contains a default list of language encodings to which you can add your own AddLanguage directives as needed. |
| `Alias` | Specifies an alias for a physical directory. The value of this directive takes the form `<Alias directory> <Physical directory>`. For instance, if you want the physical directory `/some/directory` to be accessible as `/foo` on your Web site using the URL `http://my.domain/foo`, you need the following directive: `Alias /foo /some/directory`. |
| `BrowserMatch` | Specifies environment variables based on the user agent HTTP header provided by the browser. Each browser provides a user agent header that identifies the maker and version of the browser. With the BrowserMatch directive you can define environment variables based on the value of this header. The value of the directive takes the form `<Regular expression> <Variable name>=<Variable value> <Variable name>=<Variable value> ...`. The regular expression should be a standard POSIX.2 regular expression such as `Mozilla` or `Mozilla/[3-4]`. The variable name-value pairs take one of three forms: to set a variable to 1 simply use its name as in `foo` which sets the environment variable foo to 1; to remove a variable if it is already set use the `!` symbol as in `!foo` which deletes the variable foo from the environment; and to assign an actual value to a variable, use the `=` symbol as in `foo="Some value"` which sets foo to the string Some value. |
