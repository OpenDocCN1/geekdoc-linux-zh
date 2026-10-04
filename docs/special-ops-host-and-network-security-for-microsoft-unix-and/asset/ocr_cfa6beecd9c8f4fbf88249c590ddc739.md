+   [DenyVerbs] Section If UseAllowVerbs is set to 0, only HTTP verbs not listed in this section will be allowed.

+   [AllowExtensions] Section If UseAllowExtensions is set to 1, only requests for those file extensions listed here will be allowed.

+   [DenyExtensions] Section If UseAllowExtensions is set to 0, only requests for those file extensions not here will be allowed.

+   [DenyHeaders] Section Any requests containing HTTP headers listed in this section will be rejected.

+   [DenyUrlSequences] Section Any URLs containing strings in this section will be rejected. See the sample urlscan.ini file mentioned earlier for suggested values for this section.

+   [RequestLimits] Section This section allows you to set maximum lengths for parts of incoming requests. The following settings are available:

+   MaxAllowedContentLength The maximum value allowed for the Content-Length header. The default value is 30,000,000 bytes (about 30MB). This value can be reduced significantly, especially if you are not allowing uploading of files via HTTP.

+   MaxURL This setting specifies the maximum URL length allowed. The default value is 260. This value can be reduced to the length of the longest URL on your site.

+   MaxQueryString This setting specifies the maximum length of the query string. The default is 4096 characters. This value should be reduced to a more realistic setting.

The [RequestLimits] section can also be used to limit the length of any HTTP header by creating a setting of “Max-” plus the value of the HTTP header. For example, to limit the length of the HTTP Referrer header to 50 characters, create the following setting:

```
Max-Referrer=50
```

Note that a maximum setting of zero means that URLScan will not enforce maximum lengths. To completely deny a specific header, use the [DenyHeaders] section. See the example urlscan.ini file mentioned earlier for a list of possible HTTP headers.