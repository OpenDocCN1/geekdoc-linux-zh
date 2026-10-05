Server-side Java · 97

Note that the .class extension is not included when you run the file.

# Host-based Applications

Java applets have fallen out of favor for Internet business applications. In 1997 and 1998, applets were all the rage because they delivered client-side applications over the Web. Web designers began using applets because they presented a graphical interface far superior to HTML, but they soon discovered that applets were fat clients; in fact, the code required to present “superior” interface leaned toward objectivity. Java servlets, on the other hand, are host-based. Servlets keep business logic on the server, and because the user interface for servlets is HTML, download speeds are not an issue. Some client-side logic might be required, but, more than not, you can implement client-side processing via a scripting language such as JavaScript.

Dynamic generation of HTML with Java servlets is the same strategy as CGI programs have used for several years. CGI allows you to associate a URL with a host program that can be implemented using your language of choice. However, on most platforms, each time a URL invokes a CGI program, the program is restarted, incurring normal expenses of security checks, memory allocation, and file opens. The program completes by returning an HTML response containing dynamically constructed information, that program instance is purged. Each subsequent invocation of the CGI program means the servlet is not purged; the servlet instance remains available to the Web server for invocation by multiple clients.

Legacy programmers are often reticent to believe that Java servlets outperform their C, RPG, COBOL, or third-generation architecture. Java servlets outperform legacy languages as Web application drivers because of the thread-based architecture of Java. With languages like RPG and COBOL, a different program instance is required for every browser-based request (complete with their job starts and database file opens). On the other hand, one instance of a Java servlet handles all client requests because it spawns a thread for each new request. A thread is essentially a subprocess that runs in the same space as its spawning job. Because threads are in the same address space, they can share common resources, such as file opens.

# Web Logic

Typically, a URL you enter in a Web browser refers to an HTML file within an explicit host directory: http://yourdomain/home/level1/level2/SomeHtml.html. The host simply sends the HTML file from the location specified to the client. Often, for simplicity and security, the host configuration maps a “logical” directory name to the real directory name, decreasing the length of the URL and concealing the real host name. CGI implementations also use the concept of a logical directory by mapping directory name cgi-bin to a binary of host CGI programs. When the HTTP server sees cgi-bin, it executes the program name that follows.

Web servers that support Java servlets hand over any request that has a directory qualifier of /servlet to a Web application server such as IBM’s WebSphere or Apache’s Tomcat. The Web application server, in, invokes the Java servlet qualified by /servlet.

The browser sends a URL request to the Web server in packets of information formatted according to the Hypertext Transfer Protocol (HTTP). (Note that HTTP requests and Web server are just two different names