```
#AddHandler send-as-is asis
# If you wish to use server-parsed imagemap files, use
#AddHandler imap-file map
# To enable type maps, you might want to use
#AddHandler type-map var
```

The handlers map filename extensions to a particular function. For example, the image maps are recognized from their .map extension. You may also define CGI scripts by their .cgi extensions.

```
# Action lets you define media types that will execute a script whenever
# a matching file is called. This eliminates the need for repeated URL
# pathnames for oft-used CGI file processors.
# Format: Action media/type /cgi-script/location
# Format: Action handler-name /cgi-script/location
# MetaDir: specifies the name of the directory in which Apache can find
# meta information files. These files contain additional HTTP headers
# to include when sending the document
#MetaDir .web
# MetaSuffix: specifies the file name suffix for the file containing the
# meta information.
#MetaSuffix .meta
```

```
# Customizable error response (Apache style)
# these come in three flavors
#
# 1) plain text
#ErrorDocument 500 "The server made a boo boo.
#   n.b. the ("" marks it as text, it does not get output
#
# 2) local redirects
#ErrorDocument 404 /missing.html
# to redirect to local url /missing.html
#ErrorDocument 404 /cgi-bin/missing_handler.pl
#   n.b. can redirect to a script or a document using server-side-includes.
#
# 3) external redirects
#ErrorDocument 402 http://some.other_server.com/subscription_info.html
#
```