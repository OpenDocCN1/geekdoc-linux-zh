# The Common Gateway Interface

The Common Gateway Interface (CGI) is a standard that defines the interface between the Web server and an external program. It has been around for quite awhile and is still widely used on the World Wide Web. As the Web server receives a request for a CGI program, it executes it and returns the output of the program as its response to the client.

CGI programs present dynamic information to users of a Web site, such as providing access to search engines or databases. Because they are executed by the Web server, they can get easily overloaded. In an effort to avoid this problem, you should make sure CGI programs are short and execute quickly. Most CGI programs are written in the Perl language, so they execute quickly, in addition to being powerful. Some programs may be written in C/C++, TCL (which is easy to use), and the Bourne shell (for the sake of compatibility with operating systems). The basic requirement for a CGI program is that it is executed by the user who executes the Web server.

Most executable programs are stored in a special directory such as `/cgi-bin`. Apache and other Web servers are capable of executing programs stored in other directories if they end with the `.cgi` suffix, and Apache will execute programs with any suffix as long as it’s specified in the `httpd.conf` file. Use of the `.cgi` suffix is discouraged because it can create security problems. Malicious users can install their Web directories programs that will give them access as a privileged user just by adding `.Cgi` to their files. The programs can then be executed from the Web. It is a good idea to do regular checks of the `.cgi` files, but it is easy for someone to change the name of the file and avoid detection. If you use a server that limits itself to running programs from a single directory, it is easier to control the programs that are placed in the directory. Security problems can be kept to a minimum.

The HTTP request for a CGI program is exactly the same as it is for any other type of page. Consider the following request:

```
`http://kaFka/cgi-bin/formTwo`
```

The client wants to retrieve the page `/cgi-bin/formTwo`. The Web server sees that the requested file resides in the `/cgi-bin` directory and proceeds to execute the program `formTwo`. If any output is produced, the Web server puts it into the entity body of its response.

It is sometimes necessary to send information to a CGI program so that it can be processed on the server, typically with programs used for search engines and database access. In a GET request, the information that needs to be processed by the CGI program is appended to the path name of the URL:

```
`GET /cgi-bin/find.p?dir=docs HTTP/1.0`
```

In this example, `name=value` corresponds to `dir=docs`. When the CGI program is called by the Web server, the list of name value pairs sent by the client is provided in