The Indexes option in the Options directive allows Apache to display directory listings. The `Order` (page 931) and `Allow` (page 930) directives combine to allow requests from all clients. This container is slightly less restrictive to the preceding one, although it still does not allow Apache to follow directives in .htaccess files.

# ## ADVANCED CONFIGURATION

This section describes how to configure some advanced features of Apache.

# ### REDIRECTS

Apache can respond to a request for a URI by asking the client to request a different URI. This response is called a *redirect*. A redirect works because redirection is part of the HTTP implementation: Apache sends the appropriate response code and the new URI, and a compliant browser requests the new location.

The Redirect directive can establish an explicit redirect that sends a client to a different page when a Web site is moved. Or, when a user enters the URI of a directory in a browser but leaves off the trailing slash, Apache can automatically redirect the client to the same URI terminated with a slash.

The `ServerName` directive (page 912), which establishes the name of the server, and the `UseCanonicalName` directive (page 922) are both important when a server has more than one name and needs to perform an automatic redirect. For example, assume the server with the name *zach.example.com* and the alias *www.example.com* has `ServerName` set to *www.example.com*. When a client specifies a URI of a directory but leaves off the trailing slash (*zach.example.com/dir/*), Apache has to perform a redirect to determine the URI of the requested directory. When `UseCanonicalName` is set to `On`, Apache uses the value of `ServerName` and returns *www.example.com/dir/* . With `UseCanonicalName` set to `Off`, Apache uses the name from the incoming request and returns *zach.example.com/dir/* .

# ### CONTENT NEGOTIATION

Apache can serve multiple versions of the same page, using a client's preference to determine which version to send. The process Apache uses to determine which version of a page (file) to send is called *content negotiation* . Apache supports two methods of content negotiation: MultiViews search and type maps, which can work together.

# ### TYPE MAPS

The following `AddHandler` directive from *apache2.conf* tells Apache to use any file-name ending in .var as a type map:

```
```plaintext
AddHandler type-map var
```
```