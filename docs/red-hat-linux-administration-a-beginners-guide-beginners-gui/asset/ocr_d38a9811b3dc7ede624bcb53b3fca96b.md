In this module, I discuss the process of installing and configuring the Apache HTTP Server (http://httpd.apache.org) on your Linux server. Apache is free software released under its own Berkeley Software Distribution (BSD)-style license. According to one of the most respected statistics on the Net (published by Netcraft Ltd., http://www.netcraft.com/survey), Apache has a market share of more than 60 percent. This level of respect from the Internet community comes from the following benefits and advantages provided by the Apache server software:

+   - It is stable.
+   - Several major web sites, including www.amazon.com and www.generalelectric.com, are using it.
+   - The entire program and related components are open source.
+   - It works on a large number of platforms (all popular variants of UNIX, some of the not-so-popular variants of UNIX, and even Windows).
+   - It is extremely flexible.
+   - It has shown itself to be more secure than most of the alternatives.

Before I get into the steps necessary to configure Apache, I will review some of the fundamentals of the Hypertext Transfer Protocol (HTTP) as well as some of the internal workings of Apache, such as its process ownership model. This information will help us understand why Apache is set up to work the way it does.

> **NOTE**
> Although the term "Apache" has long been used rather loosely to refer to the Apache Foundation's **httpd** server, the Apache Foundation has started branching out into a number of other programming endeavors. Its other programs are typically referred to by their full names, such as "Apache FOP" or "Apache Jakarta." The other projects of the Apache Foundation are beyond the scope of this book, so whenever I refer to a program as "Apache," you can be sure I am talking about the **httpd** server. For more information on the Apache Foundation, see http://www.apache.org.

# CRITICAL SKILL 12.1 Explaining the Mechanics of HTTP

The Hypertext Transfer Protocol (HTTP) is, of course, a significant portion of the foundation for the World Wide Web, and Apache is the server implementation of the HTTP protocol. Browsers such as Netscape Navigator, Mozilla, Opera, and Microsoft Internet Explorer are client implementations of HTTP.