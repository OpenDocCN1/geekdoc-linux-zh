# Chapter 21: Setting Up a Web Server 835

+   - Full source code, downloadable at no charge.
+   - Ease of configuration using plain-text files.
+   - Access control based on client host name/IP address or username/password combinations.
+   - Support for server-side scripting as well as CGI scripts. This includes the ability to have different users controlling script execution (to limit the vulnerability of a whole Web server if a single script is compromised).
+   - A custom API that enables external modules (for example, for extended logging capabilities, improved authentication, caching, connection tracking, and so on) to be used by the server daemon.

Apache is not the only Web server available for Fedora and other Red Hat Linux systems, but it is the one most commonly used with Linux, and is the most popular server used on the Internet according to recent Netcraft surveys (http://news.netcraft.com/archives/web_server_survey.html). In addition to Apache, Fedora and RHEL come with the lighttpd and thttpd lightweight Web servers. The TUX kernel-based HTTP server is also available, but is considered unstable for production environments.

# Other Web servers available for Fedora and RHEL

Some other Web servers that can run on Fedora and other Red Hat Linux distributions are described in the following list, with URLs that provide more detailed information.

+   - **lighttpd** — The lighttpd Web server (www.lighttpd.net) is built for security, speed, compliance and flexibility. It is particularly optimized for high performance environments because it has a low memory footprint and balances cpu-load. Sites such as YouTube, Wikipedia, and meebo have used lighttpd for some specialty Web applications.
+   - **telhttpd** — TheTelHttpd Web server (telhttpd package) is created in the Tool Command Language (TCL). Besides acting as a Web server, TelHttpd can also be used as a TCL application server.
+   - **thttpd** — The thttpd HTTP server (http://acme.com/software/thttpd) was designed to be simple, small, portable, fast, and secure. Its creators call it a tiny, turbo, throTTling HTTP server. It implements little more than the minimum needed to be HTTP/1.1 compliant, so it can run much faster than many larger Web servers under extreme loads.
+   - **XSP** — The XSP Web server (xsp package) can run ASP.NET applications, as well as related services for working with ASP.NET applications.
+   - **Zope** — In addition to being able to serve Web content, Zope includes features for adding news, membership information, and search capabilities. Originally created by Zope Corporation (www.zope.org), Zope is now available as an open source project