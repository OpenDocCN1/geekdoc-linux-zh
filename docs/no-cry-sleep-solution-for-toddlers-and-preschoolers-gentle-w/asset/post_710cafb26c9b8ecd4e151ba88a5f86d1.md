
following entry to deny access to all users. Then, in individual directories, you can allow access to certain users, groups, or hosts.

```
<Directory /var/www/html>
Order Deny,Allow
Deny from All
</Directory>
```

## URL Pathnames

Certain directives can modify or complete pathname segments of a URL used to access your site. The pathname segment of the URL specifies a particular directory or Web page on your site. Directives enable you to alias or redirect pathnames, as well as to select a default Web page. With the Alias directive, you can let users access resources located in other parts of your system, on other file systems, or on other Web sites. An alias can use a URL for sites on the Internet, instead of a pathname for a directory on your system. With the Redirect directive, you can redirect a user to another site.

```
Alias /mytrain /home/dylan/trainproj
Redirect /mycars http://www.myautos.com/mycars
```

If Apache is given only a directory to access, rather than a specific Web page, it looks for an index Web page located in that directory and displays it. The possible names for a default Web page are listed by the DirectoryIndex directive. The name usually used is index.html, but you can add others. The standard names are shown here. When Apache is given only a Web directory to access, it looks for and displays the index.html Web page located in it.

```
DirectoryIndex index.html index.shtml index.cgi
```

Apache also lets a user maintain Web pages located in a special subdirectory in the user's home directory, rather than in the main Web site directory. Using a ~ followed by the username accesses this directory. The name of this directory is specified with the UserDir directive. The default name is public_html, as shown here. The site turtle.mytrek.com/~dylan accesses the directory turtle.mytrek.com/home/dylan/public_html on the host turtle.mytrek.com.

```
UserDir public_html
```

## MIME Types

When a browser accesses Web pages on a Web site, it is often accessing many different kinds of objects, including HTML files, picture or sound files, and script files. To display these objects correctly, the browser must have some indication of what kind of objects they are. A JPEG picture file is handled differently from a simple text file. The server provides this type information in the form of MIME types (see Chapter 13). MIME types are the same types used for sending attached files through Internet mailers, such as Pine. Each kind of object is associated with a given MIME type. Provided with the MIME type, the browser can correctly handle and display the object.

The MIME protocol associates a certain type with files of a given extension. For example, files with a .jpg extension would have the MIME type image/jpeg. The TypesConfig directive holds the location of the mime.types file, which lists all the MIME types and their associated file extensions. DefaultType is the default MIME type for any file whose type cannot be determined. AddType enables you to modify the mime.type types list without editing the MIME file.

```
TypesConfig /etc/mime.types
DefaultType text/plain
```

Other type directives are used to specify actions to be taken on certain documents. AddEncoding lets browsers decompress compressed files on the fly. AddHandler maps file extensions to actions, and AddLanguage enables you to specify the language for a document. The following example marks filenames with the .gz extension as gzip-encoded files and files with the .fr extension as French language files:

```
AddEncoding x-gzip gz
AddLanguage fr .fr
```

A Web server can display and execute many different types of files and programs. Not all Web browsers are able to display all those files, though. Older browsers are the most limited. Some browsers, such as Lynx, are not designed to display even simple graphics. To allow a Web browser to display a page, the server negotiates with it to determine the type of files it can handle. To enable such negotiation, you need to enable the Multiviews option.

```
Option multiviews
```

## CGI Files

Common Gateway Interface (CGI) files are programs that can be executed by Web browsers accessing your site. CGI files are usually initiated by Web pages that execute the program as part of the content they display. Traditionally, CGI programs were placed in a directory called cgi-bin and could only be executed if they resided in such a special directory. Usually, only one cgi-bin directory exists per Web site. Distributions will normally set up a cgi-bin directory in the default Web server directory (/var/www/cgi-bin on Red Hat). Here, you place any CGI programs that can be executed on your Web site. The ScriptAlias directive specifies an alias for your cgi-bin directory. Any Web pages or browsers can use the alias to reference this directory.

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

If you want to execute CGI programs that reside anywhere on your Web site, you can specify that files with a .cgi extension are treated as executable CGI programs. You do this with the AddHandler directive (see Table 22-7). This directive applies certain handlers to files of a given type. The handler directive to do this is included in the default httpd.conf file, provided with the Apache source code files, though commented out. You can remove the comment symbol (#) to enable it.

```
AddHandler cgi-script cgi
```
