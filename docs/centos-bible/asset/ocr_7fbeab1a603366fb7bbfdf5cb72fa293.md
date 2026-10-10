# Part IV

# Networking

To make it easier to internationalize error messages and standardize how these messages are represented, the latest version of Apache includes what are referred to as *variant pages* (ending in a .var suffix). These variant pages, which offer variable output based on language, are stored in the /var/www/error directory.

```
Alias /error/ "/var/www/error/"

<IfModule mod_negotiation.c>
<IfModule mod_include.c>
  <Directory "/var/www/error">
    AllowOverride None
    Options IncludesNoExec
    AddOutputFilter Includes html
    AddHandler type-map var
    Order allow,deny
    Allow from all
    LanguagePriority en es de fr
    ForceLanguagePriority Prefer Fallback
  </Directory>
</IfModule>

ErrorDocument 400 /error/HTTP_BAD_REQUEST.html.var
ErrorDocument 401 /error/HTTP_UNAUTHORIZED.html.var
ErrorDocument 403 /error/HTTP_FORBIDDEN.html.var
ErrorDocument 404 /error/HTTP_NOT_FOUND.html.var
ErrorDocument 405 /error/HTTP_METHOD_NOT_ALLOWED.html.var
 ...
```

The *ErrorDocument* directive associates a particular error code number with a particular .var file that contains multiple possible responses based on language.

# Setting Responses to Browsers

If file extensions are not enough to determine a file's MIME type, you can define hints with the *MimeMagicFile* directive. With the *BrowserMatch* directive, you can set responses to conditions based on particular browser types:

```
#
# The following directives modify normal HTTP response behavior to
# handle known problems with browser implementations.
#
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\.0b2;" nokeepalive downgrade-1\.0 force-response-1\.0
BrowserMatch "RealPlayer 4\.0" force-response-1\.0
BrowserMatch "Java/1\.0" force-response-1\.0
BrowserMatch "JDK/1\.0" force-response-1\.0

#
```