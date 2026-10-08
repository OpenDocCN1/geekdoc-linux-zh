# Chapter 1: introduction to Web Applications and Security

Many of the technologies used to actually build applications integrate the functionality of one or more of these layers, it's often hard to distinguish one from the other in a real-world app, but they're there. For example, Microsoft's Active Server Pages (ASP) allow you to embed server-side logic within Web pages in the presentation layer, that there is no need to have a distinct executable to perform the database queries (although many sites use a distinct COM object to the database access, and this architecture may be more secure in some cases; see Chapter 9).

There is a vast diversity of techniques and technologies used to create Web n-tier logic. The most widely used (in our estimation) are categorized by vendor in Table 1-1.

Table 1-1 is mere snippet of the vast number of objects and technologies that make a typical Web Application. This includes like files, ASA files, and so on all a supporting role in keeping application logic humming (and also play a role in security vulnerabilities as, of course).

The key thing to understand all of these technologies is that they work more like executables rather than static, text-based HTML pages. For example, a request for a PHP script might look like this:

```
http://www.somite.net/file.php?id=425&format=html
```

As you see, the file.php is run just like an executable, with the items to the left of the question mark treated like additional input, or arguments. If you envision article.php

| Vendor | Technologies |
|---|---|
| Microsoft | Active Server Pages (ASP)<br>ASP.NET<br>ISAPI<br>Common Object Model (COM)<br>JavaScript |
| Sun Microsystems IBM Websphere BEA Weblogic | Java 2 Enterprise Edition (J2EE), including<br>Java Servlets<br>Java Server Pages (JSP)<br>CORBA |
| Apache Software Foundation | PHP (Hypertext Preprocessor)<br>Jakarta (server-side Java) |
| (none) | HTML<br>CGI (including Perl) |
| Table 1-1. | Selected Web Application Technologies and Vendors |