| **UserDir directive** | **Referenced path or URL** |
| --- | --- |
| `UserDir http://www.mybox.com/users` | `http://www.mybox.com/users/cjb/proj/c004.html` |
| `UserDir http://www.mybox.com/~/ *` | `http://www.mybox.com/~/cjb/proj/c004.html` |
| `UserDir http://www.mybox.com/*/html` | `http://www.mybox.com/cjb/html/proj/c004.html` |

The `UserDir` directive can also be used to explicitly allow or deny URL-to-pat hname translation for particular users. For example, it is a good idea to include the following line to avoid publishing data that shouldn't be made public:

```
UserDir disable root
```

Alternatively, use the following lines to disable the translations for all but a few users:

```
UserDir disable
UserDir enable wilhelm cjb jsmith
```

> **NOTE:** Be careful about content you publish about yourself on the Internet (names, addresses, personal information,and so on) and keep in mind that you can be held accountable for the content you publish on your Web server. When you allow others to publish on your Web server, your liability can extend to what those users publish as well. Be sure to have a clear policy about what is acceptable (and legal) to publish on your Web server and make that policy known to those you allow to use the server.

# Setting default index files for directories

The `DirectoryIndex` directive establishes a list of files that is used when an incoming request specifies a directory rather than a file. For example, say a client requests the URL `http://www.mybox.com/~jsmith/`. Because it's a directory, it is automatically translated to `http://www.mybox.com/~jsmith/`. Now that directory is searched for in any of the files listed in the `DirectoryIndex` directive. The first match (from the default list of `index.html` and `index.html.var`) is used as the default document in that directory. If none of the files exist and the `Indexes` option (as in the `httpd.conf` file) is selected, the server will automatically generate an index of the files in the directory.

```
DirectoryIndex index.html index.html.var
```

Sometimes dynamic content (such as `index.php` or `index.cgi`) will be added to the `DirectoryIndex` to make sure that dynamic content is accessed before static content when a user simply requests a domain name or directory.

# Setting directory-access control

You and your users can add an access file to each directory to control access to that directory. By default, the `AccessFileName` directive sets `.htaccess` as the file containing this