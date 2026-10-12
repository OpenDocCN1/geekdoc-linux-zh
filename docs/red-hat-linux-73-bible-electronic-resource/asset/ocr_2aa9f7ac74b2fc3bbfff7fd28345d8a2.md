| Module | Description |
| :------- | :------- |
| mod_imap | Controls inline image map files, which have a MIME type of x-httpd-imap or that are parsed by the imap handler. |
| mod_include | Implements Server-Side Includes (SSI), which are HTML documents that include conditional statements parsed by the server prior to being sent to a client. |
| mod_info | Provides a detailed summary of the server's configuration, including a list of actively loaded modules and the current settings of every directive defined within each module. |
| mod_log_agent | Enables logging of the UserAgent field from the HTTP header of incoming client requests. |
| mod_log_config | Enables a customized format for information contained within the log files. |
| mod_log_referer | Enables logging of the Referer field from the HTTP header of incoming client requests. |
| mod_mime | Alters the handling of documents based on predefined values or the MIME type of the file. |
| mod_mime_magic | Similar to the UNIX `file` command, this module attempts to determine the MIME type of a file based on a few bytes of the file's contents. |
| mod_mmap_static | If a file is not likely to change, this module enables the file to be loaded into memory when the server starts, eliminating the need to access the disk when the file is requested. |
| mod_negotiation | Provides for the conditional display of documents based upon the Content-Encoding, Content-Language, Content-Length, and Content-Type HTTP header fields. |
| mod_rewrite | Provides a flexible and extensible method for redirecting client requests and mapping incoming URLs to other locations in the file system. |
| mod_setenvif | Conditionally sets environment variables based on the contents of various HTTP header fields. |
| mod_so | The only module other than httpd core that must be statically compiled in the server, this module contains the directives necessary to implement loading dynamic shared objects. |
| mod_speling | Attempts to automatically correct misspellings in requested URLs. |
| mod_status | Provides a summary of the activities of each individual httpd server process, including CPU and bandwidth usage levels. |