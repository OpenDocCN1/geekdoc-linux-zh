# # Faster Web Applications with SCGI

**Speed up your Web applications with SCGI.**
JEROEN VERMEULEN

If you're operating a Web server, chances are, you're not merely serving up static text and images. You're likely to be running some Web applications as well, where pages are generated on the fly by some program or script using CGI (Common Gateway Interface). Think of blogging software, bug trackers, news sites and content management systems—anything that turns the browser from a document viewer into a user interface. And, you probably write or at least tweak some of these yourself.

This article shows how to build faster Web applications using an alternative to CGI called SCGI (Simple Common Gateway Interface). SCGI is a protocol, not just a program, but its authors also provide a reference implementation, which is what we use here. It includes modules to use SCGI from Apache or lightd and Python classes to help you create SCGI applications. Implementations in other languages are available, but we examine the combination of Apache 2.x and Python here.

# ## Where Does the Time Go?

Normally, a Web application runs briefly, but very frequently, in child processes of the Web server. When a client requests a page, the Web server consults its configuration and finds that the request should go to the application. It delegates the request to a child process, which in turn loads and runs the application program. The program may be a binary or a script in Perl, Python or PHP, shell commands, or just about anything else. The CGI standard defines how the program receives details about the request, including requested URL, requested body, authenticated user identity and originating IP address. The program reads these, produces a page in answer to the client's request, and exits. All this happens again at the next request.

Loading, running and exiting programs can be costly. It does make sense for sleepy programs: they may use memory without ever freeing it up again, for instance. In that case, you want the program to run briefly and then let the operating system clean up after it. But, with today's popular languages—Perl, Python, PHP, Java and shell scripts—there really aren't many problems with this. A well-written application really should be able to handle multiple requests in a single run.

# ## Faster Service with SCGI

SCGI lets your program start once and continue servicing requests for as long as it likes. It works like this: a separate server process, called an SCGI server, runs separately from the Web server and manages one Web application. The Web server forwards all requests for that application to the application's SCGI server. It passes on details about the request in much the same form as in regular CGI.

The SCGI server delegates the request to a child process, just like the Web server did with a regular CGI application. The child process also runs the application, but that's where the similarity ends. Instead of exiting after it's done with that one request, the application can sit and wait for a new one. Each of the SCGI server's child processes runs one instance of the application, each sleeping until there is work for it to do.

The SCGI server spawns a new child process when none are available to take on the latest request—up to a configurable maximum, of course. It also cleans up crashing or exiting child processes, so your Web application can still bail out if things go wrong. But, most of the time, when a request arrives, the application is ready and waiting for it. That's why Ruby on Rails, the Web application framework, comes with the option to run on SCGI; it would be too slow otherwise.

# ## Other Advantages

If the speedup isn't enough for you, there's more. The SCGI server process can be running on the same system as the Web server, but it doesn't have to be. You can offload the server by delegating some Web applications to separate systems, preferably behind a firewall where only the Web server can access them.

Even with just a single server, you can use SCGI to contain vulnerabilities. A normal CGI application starts out running under the same user identity as the Web server process. If an attacker manages to subvert a normal CGI application, your entire Web site may be at risk. An SCGI server, on the other hand, can run under its own user identity, so it can't easily affect the Web server or other applications even if it does run amok. Conversely, you don't need to give the Web server access to the application's code or data anymore; only the application as run by the SCGI server needs access. Everyone else must go through the Web server, which in turn talks to the SCGI server.

You also can run an application in a chroot environment or a virtualized server. With CGI, which quickly becomes expensive and hard to manage. When using SCGI, you start only one server process in your isolated environment—whether it's a chroot jail, a virtualized server, a different user identity or another machine—and the entire application will stay there.

# ## Installing SCGI

You need two components: the Python classes for building SCGI applications and a module for your Web server to make it “speak SCGI” to the applications. If you use Red Hat package management (RPM), you can install these using yum install python-scgi apache2-mod_scgi; users of Debian's apt can use apt-get install python-scgi