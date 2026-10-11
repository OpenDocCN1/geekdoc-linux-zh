# appendix

![](bbox=[0.0, 0.08, 0.2, 0.17])

# Dancing with Perl

Written by Alastair McGowan-Douglas

![](bbox=[0.56, 0.05, 0.79, 0.36])

Web work is a very common use of Perl. The Web is a heavily text-based medium, with plain-text HTTP being used to negotiate the transfer of plain-text HTML, XML, or JSON resources.

In the past, CGI (Common Gateway Interface) was used, but today a module called Dancer is a popular alternative. Dancer is a free, open-source micro Web application framework written in Perl that creates Web applications by building a list of HTTP verbs, routes, and methods to handle them. (See www.perlindancer.org/quickstart.)

Dancer, as well as all the other popular modern Web frameworks (such as Mojolicious and Catalyst), differs from CGI in the principal sense that your entire Dancer application is a single script that you run manually. Compare to CGI, where each CGI script would be run by the Web server, and only when requested.

The following URLs will be used to access the program example we build in this appendix.

+   * http://localhost:3000/student.cgi—CGI style
+    * http://localhost:3000/student—Modern style

The latter URL makes no mention of how the student will be served to the client; in particular, there is no mention of CGI (or PHP or ASP or anything like that). This allows us to later rework the underlying code, and clients will not have to change their bookmarks.

A major benefit of the modern style of structuring a Web application is that we don’t have to compile and run the script on every single request. We can create a single process that will handle the request and return a response. Having actually launched the application once, means it was compiled once; and if compiled once, we can make much more complex systems that can take as long as needed to actually launch, because we launch them so rarely.