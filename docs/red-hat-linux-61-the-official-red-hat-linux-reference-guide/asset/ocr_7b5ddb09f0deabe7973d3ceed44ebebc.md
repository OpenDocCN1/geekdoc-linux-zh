# 10.52. AccessName

AccessFileName names the file which the server should use for access control information in each directory. The default is .htaccess.

Immediately after the AccessFileName directive, a set of Files tags apply access control to any file beginning with a .ht. These directives deny Web to any .htaccess files (or other files beginning with .ht) for security reasons.

# 10.533. CacheNegotiatedDocs

By default, the Web server asks proxy servers not to cache any documents which were negotiated on the basis of content (that is, may change over time or because of the input from the requester). If CacheNegotiatedDocs is set to on, it disables the function and allowing proxy servers to cache documents.

# 10.534. TypesConfig

TypesConfig names the file which sets the default list of MIME type mappings (file name extensions to content types). The default TypesConfig file is /etc/mime.types. Instead of /etc/mime.types, the recommended way to add MIME type mappings is to use the AddType directive.

For information about AddType, refer to Section 10.5.58 AddType.

# 10.535. DefaultType

DefaultType sets a default type for the Web server to use for documents whose MIME types cannot be determined. The default is text/plain.

# 10.536. IfModule

<IfModule> and </IfModule> tags create a conditional container which are only activated if the specified module is loaded. Directives contained within the IfModule tags are processed under one of two conditions. The directives are processed if the module contained within the starting <IfModule> tag is loaded. Or, if an exclamation point [!] appears before the module name, the directives are processed only if the module specified in the <IfModule> tag is not loaded.

For information about Apache HTTP Server modules, refer to Section 10.7 Adding Modules.

# 10.537. HostnameLookups

HostnameLookups can be set to on, off or double. If HostnameLookups set to on, the server automatically resolves the IP address for each connection. Resolving the IP address means that the server makes one or more connections to a DNS server, adding processing overhead. If HostnameLookups is set to double, the server performs a double-reverse DNS adding even more processing overhead.

To conserve resources on the server, HostnameLookups is set to off by default.

If hostnames are required in server log files, consider performing the DNS lookups more efficiently and in bulk when rotating the Web server log files.