# Redirecting a failing URL to another Web server

If you have a multiserver Web network and often move contents from one server to another, you may face the problem of needing to redirect failing URL requests from Web server A to Web server B. There are many ways to do this: you can use the `ErrorDocument` directive, write a CGI script, or use `mod_rewrite` to rewrite the failing URLs to the other server. Using the `mod_rewrite`-based solution is less preferable than using an `ErrorDocument` directive or a CGI script. The `mod_rewrite` solution has the best performance, but is less flexible and less error-safe:

```
```apache
RewriteCond /your/docroot/%{REQUEST_FILENAME} !-f
RewriteRule ^(.+) http://Web serverB.dom/$1
```
```

The problem is that this solution will only work for pages inside the `DocumentRoot` directive. Although you can add more conditions (to handle home directories, for example), there is a better variant:

```
```apache
RewriteCond    %{REQUEST_URI} !-U
RewriteRule    ^(.+)        http://Web serverB.dom/$1
```
```

This variant uses the URL look-ahead feature of `mod_rewrite`, and will work for all types of URLs. This does have a performance impact on the Web server, however, because for every request made there is an additional internal subroutine. If your Web server runs on a powerful CPU, use this solution; if it is a slow machine, use the first approach, or, better yet, an `ErrorDocument` directive or a CGI script.

# Creating an access multiplexer

This example shows you how to create a rule set to redirect requests based on a domain type, such as .com, .net, .edu, .org, .uk, .de, and so on. The idea is to redirect the visitor to the geographically nearest Web site. This technique is employed by many large corporations to redirect international customers to an appropriate Web site or FTP server.

The first step in creating such a solution is to create a map file. For example, the following shows a text-based map file called `site-redirect.map`:

```
```
com    http://www.mydomain.com/download/
net    http://www.mydomain.com/download/
edu    http://www.mydomain.com/download/
org    http://www.mydomain.com/download/
uk     http://www.mydomain.uk/download/
de     http://www.mydomain.de/download/
ch     http://www.mydomain.ch/download/
```
```