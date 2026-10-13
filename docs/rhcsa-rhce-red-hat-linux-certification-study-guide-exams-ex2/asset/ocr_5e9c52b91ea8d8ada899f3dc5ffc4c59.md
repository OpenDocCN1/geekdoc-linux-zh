# TABLE 14-2 Main Server Configuration Directives (continued)

| Directive | Description |
|---|---|
| AddIconByEncoding | Assigns an icon for a file by MIME encoding. |
| AddIconByType | Assigns an icon for a file by MIME type. |
| AddIcon | Assigns an icon for a file by extension. |
| DefaultIcon | Sets a default icon for files not otherwise configured. |
| ReadmeName | Configures a location for a README file to go with a directory list. |
| HeaderName | Configures a location for a HEADER file to go with a directory list. |
| IndexIgnore | Adds files that are not included in a directory list. |
| AddLanguage | Assigns a language for filename extensions. |
| LanguagePriority | Sets a priority of languages if not configured in client browsers. |
| ForceLanguagePriority | Specifies action if a web page in the preferred language is not found. |
| AddDefaultCharset | Sets a default character set; you may need to change it for different languages. |
| AddType | Maps filename extensions to a specified content type. |
| AddHandler | Maps filename extensions to a specified handler; commonly used for scripts or multiple languages. |
| AddOutputFilter | Maps filename extensions to a specified filter. |
| BrowserMatch | Customizes responses to different browser clients. |

Table 14-3 specifies directives associated with Section 3: Virtual Hosts. While virtual host directives are disabled by default, I include those directives in the commented example near the end of the default httpd.conf file. While these directives were already used in other sections, you can—and generally should—customize them for individual virtual hosts to support different web sites on the same Apache server. In many cases, each virtual host stanza will include directives from the main part of the httpd.conf configuration file, customized for that virtual host.

# Basic Apache Configuration for a Simple Web Server

As described earlier, Apache looks for web pages in the directory specified by the DocumentRoot directive. In the default httpd.conf file, this directive points to the /var/www/html directory. In other words, all you need to get your web server up and running is to transfer web pages to the /var/www/html directory.