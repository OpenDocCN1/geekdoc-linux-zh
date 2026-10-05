# 914 CHAPTER 26 APACHE: SETTING UP A WEB SERVER

to display Sam's Web page. To display a user's Web page, Apache must execute permission (as www-data) for the user's home directory and the directory holding the content, and read permission for the content files.

Ubuntu provides the following configuration for user directories in the /etc/apache2/mods-available/userdir.conf file, which is disabled by default:

```
UserDir public_html
UserDir disabled root
```

Give the command a2enmod userdir to enable user directories.

Contexts: server config, virtual host
Specify in mods-available/userdir.conf
Default: none
Ubuntu: public_html, disabled root

DirectoryIndex Specifies which file Apache serves when a user requests a directory.

DirectoryIndex filename [filename ...]
where filename is the name of the file that Apache serves.

This directive specifies a list of filenames. When a client requests a directory, Apache attempts to find a file in the specified directory name matches a file in the list. When Apache finds a match, it returns that file. When this directive is absent or when none of the files by this directive exists in the specified directory, Apache displays a directory listing as specified by the IndexOptions directive (page 924).

The following DirectoryIndex directive, which Ubuntu Linux provides in the mods-enabled/dir.conf file, is enabled by default:

DirectoryIndex index.html.cgi index.pl index.php index.xhtml index.htm

This directive causes Apache to search the specified directory and return the file named index.html, index.cgi, index.pl, index.php, index.xhtml, or index.htm, index.html, index.htm, and index.htm are the names of the standard, default HTML and XHTML documents; index.cgi is a CGI document; index.pl is a Perl document; and index.php is a PHP document. The name index is standard but arbitrary.

Using headers, a client can communicate a language preference to a server. If the server can handle the preference, it determines the response from its resources. The .var is an Ubuntu addition (in apache2.conf, AddHandler type-map var, the .var extension a type map, one of the contents of content negotiation; MultiViews is the other form). For more information refer to "Content Negotiation" on page 933.

Contexts: server config, virtual host
Specify in mods-available/dir.conf
Default: index.html
Ubuntu: index.html.cgi index.pl index.php index.xhtml index.htm