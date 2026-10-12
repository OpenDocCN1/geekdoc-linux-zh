# Table 12-2 Continued

| Option | Meaning |
|---|---|
| --disable-env | Clearing/setting of ENV vars |
| --enable-mime-magic | Automatically determine MIME type |
| --enable-cern-meta | CERN-type meta files |
| --enable-expires | Expires header control |
| --enable-headers | HTTP header control |
| --enable-usertrack | User-session tracking |
| --enable-unique-id | Per-request unique IDs |
| --disable-setenvif | Base ENV vars on headers |
| --enable-tls | TLS/SSL support |
| --with-ssl | Use a specific SSL library installation |
| --with-mpm=MPM | Choose the process model for Apache to use: MPM={beos threaded prefork spmt_os2 perchild} |
| --disable-status | Process/thread monitoring |
| --disable-autoindex | Directory listing |
| --disable-asis | As-is filetypes |
| --enable-info | Server information |
| --enable-suexec | Set UID and GID for spawned processes |
| --disable-cgid | CGI scripts |
| --enable-cgi | CGI scripts |
| --disable-cgi | CGI scripts |
| --enable-cgid | CGI scripts |

Most of these options are not required for most sites. Typically, all you need is to specify the --prefix option and any options to enable or disable one or more modules. For example, say you do not want to install the CGI module on your system. You can run the configure script using the --disable-cgi --disable-cgid options to disable CGI support. Similarly, to disable the Server-Side Include (SSI) support you can use the --disable-include option.