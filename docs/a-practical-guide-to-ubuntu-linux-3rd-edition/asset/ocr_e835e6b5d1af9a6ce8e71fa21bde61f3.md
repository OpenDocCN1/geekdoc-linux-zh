# ErrorDocument *Specifies the action Apache takes when the specified error occurs.*

```
ErrorDocument code action
```

where *code* is the error code (page 948) that this directive defines a response for and *action* is one of the following:

+   *   **string**: Defines the message that Apache returns to the client.
+   *   **absolute pathname**: Points to a local script or other content that Apache redirects the client to.
+   *   **URL**: Points to an external script or other content that Apache redirects the client to.

When you do not specify this directive for a given error code, Apache returns a hardcoded error message when that error occurs.

Some examples of ErrorDocument directives follow:

```
ErrorDocument 403 "Sorry, access is forbidden."
ErrorDocument 403 /cgi-bin/uh-oh.pl
ErrorDocument 403 http://errors.example.com/not_allowed.html
```

+   *   Contexts: server config, virtual host, directory, .htaccess
+   *   Specify in httpd.conf
+   *   Default: none; Apache returns hardcoded error messages
+   *   Ubuntu: none (but see the comments in apache2.conf)

# IndexOptions *Specifies how Apache displays directory listings.*

```
IndexOptions [!=]option [!=]option] ...
```

where *option* can be any combination of the following:

+   *   **DescriptionWidth=n**: Sets the width of the description column to *n* characters. Use \* in place of *n* to accommodate the widest description.
+   *   **FancyIndexing**: In directory listings, displays column headers that are links. When you click one of these links, Apache sorts the display based on the content of the column. Clicking the link a second time reverses the order.
+   *   **FoldersFirst**: Sorts the listing so that directories come before plain files. Use only with FancyIndexing.
+   *   **HTMLTable**: Displays a directory listing in a table.
+   *   **IconsAreLinks**: Makes the icons clickable. Use only with FancyIndexing.
+   *   **IconHeight=n**: Sets the height of icons to *n* pixels. Use only with IconWidth.
+   *   **IconWidth=n**: Sets the width of icons to *n* pixels. Use only with IconHeight.
+   *   **IgnoreCase**: Ignores case when sorting names.
+   *   **IgnoreClient**: Ignores options the client supplied in the URL.