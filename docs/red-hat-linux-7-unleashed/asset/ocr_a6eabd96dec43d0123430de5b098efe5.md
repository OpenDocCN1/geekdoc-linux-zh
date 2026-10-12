# mod_imap

This module provides for server-side handling of image map files. Clickable regions are defined in a .map file. There are six directives available for use in the .map file. These are used to describe the layout of the clickable regions as well as which URLs they lead to.

# mod_include

This enables the use of Server-Side Includes on your server. See the section “Dynamic Content” later in the chapter for more information about how to use SSI.

# mod_info

The **mod_info** module provides comprehensive information about your server’s configuration. For example, it will display all the modules that are installed, as well as all the directives that are used in its configuration files.

# mod_log_agent

This enables you to log the content of the **UserAgent** header from HTTP requests. Using this information allows you to see which Web browsers visitors to your site are using.

# mod_log_config

This module allows you to define how your log files should look. See the section “Logging” for further information about this subject.

# mod_log_referer

This enables you to log the referer part of an HTTP request.

> **Note**
> As of Apache 1.3.5, this module is deprecated. Use the CustomLog directives instead. See the section on logging for more information on CustomLog.

# mod_mime

This module tries to determine the MIME type of files from their extensions.