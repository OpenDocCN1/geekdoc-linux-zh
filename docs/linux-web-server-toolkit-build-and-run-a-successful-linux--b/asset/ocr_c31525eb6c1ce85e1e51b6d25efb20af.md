# Chapter 13: Maintaining Statistical Data for Your Site 365

# # Understanding Server Log Files

If you reviewed Chapter 11, you may remember a little about the log files that are written by the Web server. Almost any Web server creates log files in the same format. This format, the Common Log Format, was defined by the early Web designers at CERN and the NCSA Mosaic project.
Every file you sent from your Web server generates a log entry. A log entry might look like this:

```
dynamo.target.org - [02/Sep/1997:14:02:22 -0800] GET
/Index.html HTTP/1.0 200 44398
```

The default entry contains the following fields:

+   - The hostname of the person requesting the file, as reported by the browser. Depending on how your configuration files are set, this might be recorded as the IP address of the user's machine instead of this hostname. An additional feature of Apache allows you to have the Web server do a reverse lookup of each hostname to be that every system that requests a file is really who it claims to be. This security feature uses a lot of processor and network bandwidth, however, and is not necessary on most sites.
- The username given to permit access to the requested file. This field is only used if a file has user-level authentication set in a <LIMIT> container in the access.conf file.
- User identification information, as returned from the requesting host, using identd security. This authorization information is rarely used.
- The date and time when the transfer was completed (recorded in Universal Time, with an offset hour based on your local time zone).
- The request string from the browser. This will usually be a GET command, which includes the name of the file to be sent and the pathname it was requested by the browser (thus relative links will not include a full path starting at your document root).
- The http protocol code that was sent with the data. For all entries in the access log, this will likely be 200, the code for "OK." Other codes, such as "File Not Found," "Insufficient Access Rights," "File Moved," and so forth, are considered error conditions and are recorded in the error log file.