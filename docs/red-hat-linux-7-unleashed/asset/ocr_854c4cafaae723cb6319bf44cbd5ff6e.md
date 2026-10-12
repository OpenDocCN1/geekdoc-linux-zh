To create password files for use with `mod_auth_dbm` you will need to use the **htdigest** utility. It has more or less the same functionality as the `htpasswd` utility. See the man page of **htdigest** for further information.

> **Caution**
> This module is still considered experimental!

# ### mod_autoindex

If you have not provided a default HTML file for a directory and have enabled directory indexing, this module will dynamically create a file list for the directory in question. This list will be rerendered in a user-friendly manner similar to those lists that FTP provides. There are many options that will provide you with the ability to fine-tune every aspect of the look and feel of the directory listing.

# ### mod_bandwidth

This module provides bandwidth usage limitation. It enables basic traffic shaping for replies so that the server will not become overloaded when there are too many requests. This can be applied either to parts of the server or the whole server. You may apply the module based on file size, location or domain of the client, and the location or directory of the requested material.

This is one of the third-party modules that Red Hat has added that are generally not part of the Apache distribution.

# ### mod_cern_meta

This module gives you the ability to add additional HTTP headers to each HTTP response. You can configure Apache so that the contents of files with certain extensions, usually `.meta`, will be included together with any other HTTP headers that Apache generates.

# ### mod_cgi

This module allows you to execute CGI scripts on your server. See the section on dynamic content for more information about how to use CGIs.