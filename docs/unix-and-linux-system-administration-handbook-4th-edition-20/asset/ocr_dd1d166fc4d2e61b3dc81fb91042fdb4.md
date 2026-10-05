# 23.1 WEB HOSTING BASICS

Hosting a web site isnt substantially different from providing any other network service. A daemon listens for connections on TCP port 80 (the HTTP standard), accepts requests for documents, and transmits them to the requesting user's browser. Many of these documents are generated on the fly in conjunction with databases and application frameworks, but that's incidental to the underlying HTTP protocol.

# Resource locators on the web

Information on the Internet is organized into an architecture defined by the Internet Society (ISOC). This well-intended (albeit committee-mined) organization helps ensure consistency and interoperability throughout the Internet.

ISOC defines three primary ways to identify a resource: Uniform Resource Identifiers (URIs), Uniform Resource Locators (URLs), and Uniform Resource Names (URNs). URLs and URNs are really specialized types of URIs, as illustrated in Exhibit A.

# Exhibit A Uniform resource taxonomy

![](bbox=[0.25, 0.485, 0.538, 0.552])

So what's the difference?

+   * URLs tell you how to locate a resource by describing its primary access mechanism (e.g., http://admin.com).
* URNs identify ("name") a resource without implying its location or telling you how to access it (e.g., urn:isbn:0-13-020601-6).

When do you call something a URI? If a resource is only accessible through the Internet, refer to it as a URL. If it could be accessed through the Internet or through other means, then you're using a URI.

# Uniform resource locators

Most of the time, you'll be dealing with URLs, which describe how to access an object through five basic components:

+   * Protocol or application
* Hostname
* TCP/IP port (optional)
* Directory (optional)
* Filename (optional)