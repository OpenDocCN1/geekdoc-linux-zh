For UserDir to work, the mod_userdir module must also be loaded (which it is by default). There are two ways in which the UserDir directive can handle an incoming request that includes a username (e.g., ~/cjb). One possible format identifies the physical pathname of the individual user's publicly accessible directories. The other can specify a URL to which the request is re-directed. A few examples are presented in Table 20-4, using the URL www.mybox.com/~cjb/proj/c004.html as a sample request.

# **TABLE 20-4**
UserDir Pathname and URL Examples

UserDir Directive | Referenced Path or URL
UserDir public_html | ~/cjb/public_html/proj/c004.html
UserDir /public/*/www | /public/cjb/WWW/proj/c004.html
UserDir /usr/local/web | /usr/local/web/cjb/proj/c004.html
UserDir http://www.mybox.com/users | http://www.mybox.com/users/cjb/proj/c004.html
UserDir http://www.mybox.com/~/ | http://www.mybox.com/~cjb/proj/c004.html
UserDir http://www.mybox.com/*/htm | http://www.mybox.com/cjb/html/proj/c004.html

The UserDir directive can also be used to explicitly allow or deny URL-to-pathname translation for particular users. For example, it is a good idea to include the following line to avoid publishing data that shouldn't be made public.

```
UserDir disable root
```

Alternatively, use the following lines to disable the translations for all but a few users:

```
UserDir disable
UserDir enable wilhelm cjb jsmith
```

> **NOTE** You should always be careful about content you publish about yourself on the Internet (names, addresses, personal information, etc.) and also keep in mind that you can be held accountable for the content you publish on your Web Server. When you allow others to publish on your Web Server, your liability can extend to what those users publish as well. Be sure to have a clear policy about what is acceptable (and legal) to publish on your Web Server, and give that information to those you allow to use the server.

# Setting Default Index Files for Directories

The *DirectoryIndex* directive establishes a list of files that is used when an incoming request specifies a directory rather than a file. For example, a client requests the URL