| UserDir Directive | Referenced Path or URL |
| :---------------- | :--------------------- |
| UserDir public_html | ~cjb/public_html/proj/c004.html |
| UserDir /public/*/WWW | /public/cjb/WWW/proj/c004.html |
| UserDir /usr/local/web | /usr/local/web/cjb/proj/c004.html |
| UserDir http://www.mybox.com/users | http://www.mybox.com/users/cjb/proj/c004.html |
| UserDir http://www.mybox.com/~* | http://www.mybox.com/~cjb/proj/c004.html |
| UserDir http://www.mybox.com/*/html | http://www.mybox.com/cjb/html/proj/c004.html |

The UserDir directive can also be used to explicitly allow or deny URL-to-path name translation for particular users. For example, it is a good idea to include the following line to avoid publishing data that shouldn’t be made public:

```
```
UserDir disable root
```
```

Alternatively, use the following lines to disable the translations for all but a few users:

```
```
UserDir disable
UserDir enable wilhelm cjb jsmith
```
```

The DirectoryIndex directive establishes a list of files that is used when an incoming request specifies a directory rather than a file. For example, a client requests the URL http://www.mybox.com/~jsmith. Because it’s a directory, it is automatically translated to http://www.mybox.com/~jsmith/. Now that directory is searched for any of the files listed in the DirectoryIndex directive. The first match (from the default list of index.html and index.html.var) is used as the default document in that directory. If none of the files exist and the Indexes option (as in the httpd.conf file) is selected, the server will automatically generate an index of the files in the directory.

```
```
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
# The index.html.var file (a type-map) is used to deliver content-
# negoiated documents.  The MultiViews Option can be used for the
# same purpose, but it is much slower.
#
DirectoryIndex index.html index.html.var
```
```