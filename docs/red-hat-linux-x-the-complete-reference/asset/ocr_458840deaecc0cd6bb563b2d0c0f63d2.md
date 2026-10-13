**mime.types** file, which lists all the MIME types and their associated file extensions. **DefaultType** is the default MIME type for any file whose type cannot be determined. **AddType** enables you to modify the **mime.type** types list without editing the MIME file.

```
TypesConfig /etc/mime.types
DefaultType text/plain
```

Other type directives are used to specify actions to be taken on certain documents. **AddEncoding** lets browsers decompress compressed files on the fly. **AddHandler** maps file extensions to actions, and **AddLanguage** enables you to specify the language for a document. The following example marks filenames with the .gz extension as gzip-encoded files and files with the .fr extension as French language files:

```
AddEncoding x-gzip gz
AddLanguage fr .fr
```

A Web server can display and execute many different types of files and programs. Not all Web browsers are able to display all those files, though. Older browsers are the most limited. Some browsers, such as Lynx, are not designed to display even simple graphics. To allow a Web browser to display a page, the server negotiates with it to determine the type of files it can handle. To enable such negotiation, you need to enable the **Multiviews** option.

```
Option multiviews
```

# CGI Files

Common Gateway Interface (CGI) files are programs that can be executed by Web browsers accessing your site. CGI files are usually initiated by Web pages that execute the program as part of the content they display. Traditionally, CGI programs were placed in a directory called **cgi-bin** and could only be executed if they resided in such a special directory. Usually, only one **cgi-bin** directory exists per Web site. Distributions will normally set up a **cgi-bin** directory in the default Web server directory (/var/www/cgi-bin on Red Hat). Here, you place any CGI programs that can be executed on your Web site. The **ScriptAlias** directive specifies an alias for your **cgi-bin** directory. Any Web pages or browsers can use the alias to reference this directory.

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

If you want to execute CGI programs that reside anywhere on your Web site, you can specify that files with a .cgi extension are treated as executable CGI programs. You do this with the **AddHandler** directive (see Table 22-7). This directive applies certain handlers to files of a given type. The handler directive to do this is included in the default **httpd.conf** file, provided with the Apache source code files, though commented out. You can remove the comment symbol (#) to enable it.

```
AddHandler cgi-script cgi
```

Table 22-7: CGI Directives

| Directive | Description |
|---|---|
| `Action action-type cgi-script` | Adds an action, which activates `cgi-script` when `action-type` is triggered by the request. |
| `AddHandler handler-name extension extension ...` | Maps the filename extensions `extension` to the handler `handler-name`. |
| `RemoveHandler extension extension ...` | Removes handler associations for files with the given extensions. This allows `.htaccess` files in subdirectories to undo any associations inherited from parent directories or the server configuration files. |