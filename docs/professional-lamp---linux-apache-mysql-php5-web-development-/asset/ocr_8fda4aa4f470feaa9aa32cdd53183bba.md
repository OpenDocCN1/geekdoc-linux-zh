| REQUEST_FILENAME | Full local file system path for the item matching the HTTP request | 
| --- | --- | 
| IS_SUBREQ | Whether or not the request being processed is an internal sub-request; the value will be "true" if the request is a subrequest, "false" if not | 
| HTTPS | A value of "on" indicates SSL/TLS is being used, "off" if not |

To use any of the variables from that long list, you wrap the variable name in curly braces, and prefix with a percent sign, like so:

```
%{SCRIPT_FILENAME}
```

To see RewriteCond in action, first rewrite a RewriteRule to make use of RewriteCond . The old rule looked like this:

```
# Rewrite /category/ to catalog.php
RewriteRule ^\(w+\)/?$ catalog.php?cat=$1&item=$2
```

To accomplish the same goal using RewriteCond in conjunction with RewriteRule , use the following:

```
# Rewrite /category/item/ to catalog.php
RewriteCond %{SCRIPT_FILENAME} ^/(w+)/?(w+)/?$
RewriteRule .* catalog.php?cat=$1&item=$2
```

Notice how the server variable SCRIPT_FILENAME was used as the test input string. Combining RewriteCond with RewriteRule using these server variables, you can come up with some interesting combinations. The following checks to see if the user's browser can accept XHTML MIME types, and if so, changes the MIME type header sent for .html files:

```
RewriteCond %{HTTP_ACCEPT} application/xhtml+xml
RewriteRule .*.html$ - [T=application/xhtml+xml]
```

Another helpful feature of RewriteCond is the ability to chain multiple lines together. When listing multiple RewriteCond statements in a row, they are each treated like a programmatic AND— the RewriteRule at the end will only process if all the RewriteCond matches return true. The previous set of rules could be rewritten using multiple RewriteCond statements, like this:

```
RewriteCond %{HTTP_ACCEPT} application/xhtml+xml
RewriteCond %{SCRIPT_FILENAME} \.html$
RewriteRule .*. - [T=application/xhtml+xml]
```

In addition to the standard string-versus-regex comparisons, you can actually make simple comparison and system-check conditionals with RewriteCond . To compare your input string against another simple string, you can use the following as your conditional pattern:

```
<CondPattern
>CondPattern
=CondPattern
```