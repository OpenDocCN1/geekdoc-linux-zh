# Hacking Exposed Web Applications

Length: 458 [text/html]
OK
100% @ 22.36 KB/s
...(continues for entire site)...

The "r," or "recursive," option instructs wget to follow every link on the home page. This will create a "www.victim.com" directory and populate directory with every HTML file and directory for the site. A major advantage of wget is that it follows every link possible. It will, download the output for every argument that the application passes to a page. For example, the viewer.asp file for a site might be downloaded four times:

+   - viewer.asp@ID=555
- viewer.asp@ID=7
- viewer.asp@ID=42
- viewer.asp@ID=23

The @ symbol represents the ? delimiter in the original URL. The ID is the first argument (parameter) passed to the viewer.asp file. Some sites may require more advanced options such as support for proxies and HTTP Basic Authentication. Authentication is protected by:

```
[root@ndle] wget -r --http-user:dwayne --http-path:wodoelf \
> https://www.victim.com/secure/
--20:19:11-- https://www.victim.com/secure/
=> 'www.victim.com/secure/index.html'
```

Connecting to www.victim.com... connected!
HTTP request sent, awaiting response... 200 OK
Length: 251 [text/html]
100% @ 21.99 KB/s
OK
...continues for entire site...

Wget has a simple purpose: retrieve files from a Web Site. Sifting through the results requires some other simple command-line tools available on any UNIX system or Windows Cygwin.

# Teleport Pro

| Pro: | Easy to use, no SSL support, commercial |
| Con: | No capability to search HTML for comments, e-mail addresses, etc. |
| Final Analysis: | Good for finding static files |

Of course, for Windows users there is always something GUI. Teleport Pro (http://www.tenmax.com/teleport/pro/home.htm) brings a graphical interface to the function of wget and sifting tools for gathering information.