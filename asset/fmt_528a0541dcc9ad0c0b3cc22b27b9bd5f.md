
```
Content-Length: 7044

Content-Type: text/html

<contents of your default file appear here>

Connection closed by foreign host.
```

In this case, we told the server we were going to speak HTTP protocol version 1.1 and named the virtual host from which we were requesting information. The server returned a status code (`HTTP/1.1 200 OK`), its idea of the current date and time, the name and version of the server software it was running, the date that the requested file was last modified, the length of the requested file, and the requested file's content type. The header information is separated from the content by a single blank line.

## Content generation on the fly

In addition to serving up static documents, an HTTP server can provide the user with content that has been created on the fly. For example, if you wanted to provide the current time and temperature to users visiting your web site, you might have the HTTP server execute a script to obtain this information. This amaze-the-natives trick is often accomplished with the Common Gateway Interface, or `CGI`.

`CGI` is not a programming language but rather a specification by which an HTTP server exchanges information with other programs. `CGI` scripts are most often written in `Perl`, `Python`, or `PHP`. But really, any programming language that can perform real-time I/O is acceptable.

## Embedded interpreters

The `CGI` model provides complete flexibility in that the web developer is free to use any interpreter or scripting language. Unfortunately, starting a separate process for every script call can be a performance nightmare on busy web servers that serve a significant amount of dynamic content.

In addition to supporting external `CGI` scripts, many web servers define a plug-in architecture that allows script interpreters such as `Perl` and `PHP` to be embedded within the web server itself. This bundling significantly increases performance because the web server no longer needs to fork a separate process to deal with each script request. The architecture is largely invisible to script developers. Whenever the server sees a file ending in a specified extension (such as `.pl` or `.php`), it sends the contents of the file to the embedded interpreter to be executed. Table 23.2 on the next page lists some common embedded interpreters that run inside Apache.

## FastCGI

Another trick you can use in some situations is `FastCGI` (`fastcgi.com`). This module improves the performance of scripts by starting them once and then leaving them running to service multiple requests. This arrangement amortizes the cost of starting the interpreter and parsing the script across multiple requests. It can be faster than running the interpreter inside Apache itself.

Unfortunately, scripts must be modified to understand and conform to this new way of interacting with the web server. The basic protocol is easy to implement, but `FastCGI` scripts cannot afford to be sloppy about memory management. Loose ends cause the script's memory footprint to grow over time. Another potential hazard is the persistence of data across requests; programmers must ensure that requests cannot interact. Web developers will need to weigh whether the performance improvement from `FastCGI` is worth the extra effort and risk.

Some administrators prefer `FastCGI` to embedded interpreters because individual scripts can be restarted without affecting the rest of the system when they go awry. With embedded interpreters, you may need to restart the entire web server if one interpreter starts acting up.

### Table 23.2 Embedded scripting modules for the Apache web server

| Language | Name of embedded interpreter | Learn more |
|---|---|---|
| `Perl` | `mod_perl` | `perl.apache.org` |
| `Python` | `mod_python` | `modpython.org` |
| `PHP` | `mod_php` (traditional) | `apache.org` |
|  | `Zend server` (commercial accelerator) | `zend.com` |
| `Ruby on Rails` | `Phusion Passenger` (aka `mod_rails` or `mod_rack`) | `modrails.com` |

## Script security
