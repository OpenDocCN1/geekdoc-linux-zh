# Linux Web Server Toolkit

Because it provides more features at a lower level, it's also not subject to the same restrictions – safeguards – as Java and JavaScript. That means that a plug-in you develop with the API can crash the Web server. Typical uses of API include:

+   * Customizing access control mechanisms
* Customizing error handling mechanisms
* Customizing request or error logging
* Initializing shared resources
* Modifications to the normal HTTP request-response process, including maintaining stateful systems

Although FastTrack provides several methods for programming or integrating programs with the Web server, the Netscape API is the fastest-executing, most powerful method available. CGI scripts in Perl or even C don't have as high performance, and Java or JavaScript won't even come close. For the best performance, the most flexibility, and the greatest power, use plug-in APIs.

Much like the UNIX model itself, API functions provide many small tools, carefully designed to do one task well. This provides a great deal of control over the server's behavior. Developers can implement their own systems for authentication, client tracking, access control, error logging, or other features.

# Using APIs to Your Advantage

The APIs for both Netscape and Apache are written in C, so any modules you want to write will be written in C as well. The following sections provide brief outlines of the functionality and operation of the Apache and Netscape APIs. You'll note from these outlines and also from the documentation included with the Apache and FastTrack servers that the functions available with the Apache system provide more flexibility and perhaps more power in the API, as well as more concrete examples, than the Netscape API.

The Netscape API, on the other hand, is not as rich, but probably easier to use. It doesn't advance as rapidly or for as deep or as wide an impact on the server's functionality. And, unfortunately, the Netscape Programmer's Guide has fewer code fragments to help you along the path than does the Apache documentation. That part is regrettable and not dictated by the commercial nature of the Netscape products.

Anyway, both APIs provide great capabilities and flexibility to you as any you add features to your Web server. Use the information below to get a feel for the APIs, then refer to the documentation for each product for more complete information, including lists of functions and more technical detail than I can provide here.