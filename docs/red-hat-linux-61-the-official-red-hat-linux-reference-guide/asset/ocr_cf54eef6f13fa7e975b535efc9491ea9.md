# 10.2.2.2. Logging

The following logging directives have been removed:

+   - AgentLog
- ReferrerLog
- ReferrerIgnore

However, agent and refer logs are still available using the CustomLog and LogFormat directives. For on this topic, refer to the following documentation on the Apache Software Foundation’s website:

+   - http://httpd.apache.org/docs-2.0/mod/mod_log_config.html#customlog
- http://httpd.apache.org/docs-2.0/mod/mod_log_config.html#logformat

# 10.2.2.3. Directory Indexing

The deprecated FancyIndexing directive has been removed. Same functionality is available through the FancyIndexing option within the IndexOptions directive.

The new VersionSort option to the IndexOptions directive causes files containing version numbers to be sorted in a more natural way. For example, httpd-2.0.6.tar appears after httpd-2.0.36.tar in a directory page.

The defaults for the ReadName and HeaderName directives have changed from HEADER to README.html and HEADER.html.

For on this topic, refer to the following documentation on the Apache Software Foundation’s website:

+   - http://httpd.apache.org/docs-2.0/mod/mod_autoindex.html#indexoptions
- http://httpd.apache.org/docs-2.0/mod/mod_autoindex.html#readmename
- http://httpd.apache.org/docs-2.0/mod/mod_autoindex.html#headername

# 10.2.2.4. Content Negotiation

The CacheNegotiatedDocs directive now takes the argument on or off. Existing instances of CacheNegotiatedDocs should be replaced with CacheNegotiatedDocs on.

For on this topic, refer to the following documentation on the Apache Software Foundation’s website:

+   - http://httpd.apache.org/docs-2.0/mod/mod_negotiation.html#cachenegotiateddocs

# 10.2.2.5. Error Documents

To use a hard-coded message with the ErrorDocument directive, the message should be enclosed in a pair of double quotation marks [*], rather than just preceded by a double quotation mark as required in Apache HTTP Server 1.3.

To migrate an ErrorDocument setting to Apache HTTP Server 2.0, use the following structure:

```
ErrorDocument 404 "The document was not found"
```