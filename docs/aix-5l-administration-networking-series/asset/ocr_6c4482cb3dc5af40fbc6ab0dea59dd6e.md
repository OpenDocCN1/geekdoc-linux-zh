Access may also be limited in terms of the host, or network, where the user is logically located. This is accomplished via the Order, Allow, and Deny directives. For example:

```
```
Order deny, allow
Allow from 10.10.120,
Deny from cse.froth.edu
```
```

This example gives Deny directives preference over Allow directives, then explicitly allows connections from users on the 10.10.120 network and denies users coming from cse.froth.edu. These directives are typically scoped to a specific directory tree or virtual host.

# ## URI Mapping Directives

When a document root is set, this implies a valid URI tree for the host rooted at the DocumentRoot directory; any valid file or directory below the DocumentRoot directory becomes part of a valid URI. However, it is often desirable to map other files and directories into this space. Two such mapping directives are Alias and ScriptAlias. Enabling aliases simply maps one valid subtree into another space. Optional directives like Indexes and FollowSymLinks will still need to be activated for the new directory for these features to work properly (see Example 18-5).

# **Example 18-5**

```
```
<Directory /usr/local/myhtdocs/>
Options Indexes
AllowOverride none
</Directory>
Alias        /mydocs/    /usr/local/myhtdocs/
```
```

# ## MIME Types

The Web is a multimedia service capable of incorporating any arbitrary data format. Because of the design of the HTTP protocol, many data types cannot be transferred without conversion to another format. This is accomplished using MIME format headers. MIME allows the Web server to convert the document to a format supported by HTTP and the Web client to convert it back to the original format, all without input from the Web client user. Conversion and display of many data types, such as IPG images, are often supported directly by the browser. When the browser encounters a MIME type that it does not support, it relies on helper applications to display or otherwise process the data. Apache uses the mime.types file to determine the MIME type headers to send to a client requesting data, so that the client knows how to format the data. Additional types can be added by either editing this file, or by using the AddType directive in the httpd.conf file.