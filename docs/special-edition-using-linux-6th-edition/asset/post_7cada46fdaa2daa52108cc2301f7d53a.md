
- **AddIconByType**—Assign an icon by MIME file type. The type is determined by the settings in the `mime.types` configuration file.
- **AddIconByEncoding**—Assign an icon by MIME encoding. File encoding types are defined by `AddEncoding` directives.
- **AddAlt**—Assign alt string by file extension.
- **AddAltByType**—Assign alt string by MIME file type.
- **AddAltByEncoding**—Assign alt string by MIME encoding.
- **DefaultIcon**—Specify the icon to use, when no other icon can be found for this entry.

The syntax for the Add... directives is as follows:

```
<directive> <icon> <match> [<match2> ...]
```

For any of the AddIcon... directives, for the icon field you can specify either just the icon filename, or a combination of alt string and icon filename. This enables you to bypass use of the AddAlt... directives, if you want. The icon filename is expressed as a path relative to the Web server document tree, not relative to your local filesystem. Also, an AddIcon directive can use the string `^DIRECTORY^` to match directory entries. The following example shows several different icon assignment lines. Some of these overlap in functionality, but they are shown for illustrative purposes:

```
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/text.gif .txt
AddIconByType /icons/apache/text.gif text/*
AddAltByType "TXT" # text/*
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (HTM,/icons/about.gif) text/html
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip
AddIcon (DIR,/icons/folder.gif) ^DIRECTORY^
DefaultIcon /icons/unknown.gif
```

The icon directives are processed in the order that they occur in the httpd.conf file. The Web server uses the first match that it finds as the icon for a file. Therefore, place more specific directives earlier in the file for the matching to work.

You can, of course, add your own icon files if you want to completely customize the look of the directory listing pages. The icons need to be in .gif or .jpg format and reside in a directory somewhere in the document tree. The default icons provided with Apache are in the directory `/usr/local/apache/icons`, and are 20×22 8-bit color GIF files. These icons use very few colors (a good idea) and a transparent background.

## USING DESCRIPTIONS

The Description column in a fancy directory listing has a short description of each entry. The Web server determines the value for this field based either on AddDescription directives used in server configuration files, or on the title of the document, if it is an HTML file.

Use the AddDescription directive to add a description for an entry. For example, the following line adds a description for the file foo.txt at the root of the document tree:

```
AddDescription "foo text file" /foo.txt
```

The server can automatically add descriptions to the directory listing, based on the title of HTML documents in the directory. Add the ScanHTMLTitles option to the IndexOptions directive in httpd.conf to have the server do this. Note that this causes the server to read each HTML file in the directory and parse out the HTML title every time the directory is read. This takes a relatively long time, and should not be used on busy Web sites.

## CONTROLLING COLUMNS AND DIRECTORY FORMATTING

The IndexOptions directive enables you to control several other aspects of the fancy directory listing. Table 33.4 shows the options you can use and their effect on the listing page.

**Table 33.4 — Options to Control Fancy Directory Listings Using IndexOptions**

| Option | Meaning |
| --- | --- |
| `IconHeight=pixels` | The Web server includes the height of icons in the IMG tag used in the directory index page. This can speed up processing of the page by client browsers. |
| `IconWidth=pixels` | The Web server includes the width of icons in the IMG tag used for directory indexes. |
| `IconsAreLinks` | This makes the icons part of the link to the entry, so the user can click either the entry name or the icon to access it. |
| `NameWidth=n\|*` | Indicates the width of the filename column. If * is used, the column is sized automatically. |
| `ScanHTMLTitles` | The server scans HTML files for their titles, to be used in the Description column. |
| `SuppressDescription` | Hide the Description column. |
| `SuppressLastModified` | Hide the Last Modified column. |
| `SuppressSize` | Hide the Size column. |
| `SuppressColumnSorting` | Do not make the column headings links that can be used to sort the listing by that column. |
| `SuppressHTMLPreamble` | Do not precede the file specified by HeaderName with the standards HTML preamble (HTML, HEAD, and so on). This allows you more flexibility in controlling the page output with the header file. |

## CUSTOMIZING ERROR MESSAGES

The Web server automatically generates error message responses for certain error conditions. However, you can customize the error response for your Web site to provide your own messages (and look and feel) to remote clients when things go wrong.

Use the ErrorDocument directive to customize the error response for a particular error condition. This directive can be used multiple times, to specify a response for each different error code that the server generates. Common error codes used by the Web server are shown in Table 33.5.

**Table 33.5 — Common HTTP Error Codes**

| Error Code | Summary | Meaning |
| --- | --- | --- |
| 400 | Bad Request | The request from the client was malformed. |
| 401 | Unauthorized | Client must provide a name and password to access the item. Note that the error response for this code cannot be customized because the client automatically displays a login prompt (and not the returned page) when it receives this error from the server. |
| 402 | Payment Required | Access to the requested item requires that the client provide some kind of payment. |
| 403 | Forbidden | Client is not allowed to access the item. Providing a name and password does not help. |
| 404 | Not Found | The server did not find a document or directory matching the URL submitted by the client. |
| 500 | Fatal Error | The server encountered some unresolvable condition and could not fulfill the request. |
| 501 | Not Implemented | The server does not support the requested functionality. |
| 502 | Temporary Overload | The server cannot service the request because of high load. It can possibly service the request at a later time. |

The error document can be specified in several ways. First, you can specify just a string to return to the user as the value for the ErrorDocument. You can also refer to a local file to return a static error page, or to a CGI script to generate one at the time of the request. Using a CGI script enables you to customize the response to exactly match your situation because the script can examine information about the client, its request, and the local filesystem at the time that the request is made. Finally, you can also specify an external document as an error response.

For each ErrorDocument directive, specify the error code, and then the item with which you want the server to respond for that error. Following are some examples of ErrorDocument lines:

```
ErrorDocument 400 "Hey, you sent invalid request."
ErrorDocument 402 http://www.example.com/pay_me.html
ErrorDocument 500 /fatal.html
ErrorDocument 404 /cgi-bin/missing.pl
```

## CONFIGURING SETTINGS ON A PER DIRECTORY BASIS

When you use the configuration directives for controlling file information, directory indexing, error responses, and authorization (discussed later) in httpd.conf, they apply to the entire document tree that the Web server provides. However, you can also apply these directives to specific directories and files on your system.

There are a few different reasons that the server supports per directory customizations in this way. First, you might want to have some directories on your Web site available to the general public, whereas other files and directories are restricted to a specific set of users. In addition to security-specific directives, many other directives have important security ramifications. For instance, you usually do not want the general public to see the contents of the directories in your document tree. Therefore, it is customary to disable directory indexing for the part of your document tree that is accessible to any remote user. You might still want, however, to allow indexing for users within your organization.

Sometimes the content of a Web site is maintained by different organizations in a company. In this case, they might have different policies and conventions for controlling their part of the site. For example, one department might use server-parsed HTML files for some of their content, whereas another might not. Because server-parsed HTML files require extra processing by the server, it is wise to limit its use to only the part of the document tree that needs it.

The use of per directory settings allows for fine-grained control over the presentation, handling, and access control of the server document tree.

### PER DIRECTORY OPTIONS

Some of the main options that can be configured on a per directory basis are controlled with the Options directive. This directive enables you to set many policies with regard to directories:

- **All**—All options except for `MultiViews`
- **ExecCGI**—Execution of CGI scripts is allowed.
- **FollowSymLinks**—The server follows symbolic links in this directory. This can be a potential security risk.
- **Includes**—Server-side includes (server-parsed HTML) are allowed.
- **IncludesNOEXEC**—Server-side includes are allowed, but certain directives are not processed (`#exec` and `#include`).
- **MultiViews**—Allows the server to select a document that best matches the client’s request when the requested file does not exist. This is referred to as content-negotiation, and is covered in the online manual at http://www.apache.org/docs/content-negotiation.html.
- **SymLinksIfOwnerMatch**—Allows the server to follow a symlink if the target of the link and the link have the same owner ID.

> **Caution**
> 
> Most options in this list have important security consequences. For example, allowing any kind of execution by the Web server (for example, use of `ExecCGI` and `Includes`) might lead to situations in which unauthorized users can allow more clients to run dangerous programs or scripts. Consult the online documentation for each of these options for information about the security ramifications before using them on a multiuser system.
