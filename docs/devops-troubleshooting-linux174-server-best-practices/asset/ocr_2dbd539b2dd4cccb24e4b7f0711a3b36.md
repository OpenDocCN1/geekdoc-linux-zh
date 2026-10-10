# **Test a Web Server from the Command Line 147**

Since we just want to test basic web server functionality, we don't necessarily need to get into any of curl's more sophisticated command-line options. In fact, testing a web server from curl can be as simple as typing curl and then the URL to load:

```
$ curl http://www.example.net
<html><body><h1>It works!</h1>
<p>This is the default web page for this server.</p>
<p>The web server software is running but no content has been added, yet.</p>
</body></html>
```

In this example, you can see the default web page created by an Apache web server. If for some reason the web server were unreachable, you would see something like

```
$ curl http://www.example.net
curl: (7) couldn't connect to host
```

By default, curl will just output the contents of the web page you requested, but often when you troubleshoot web servers you'd like to get extra data, such as the HTTP status code (more on that later), how long the request took, how much data was transferred, and so on. Curl offers a -w option that lets you pull additional data about the request and display it on the screen. So, for instance, if you wanted to see the HTTP status code for a request, you could type

```
$ curl -w "␈%{http_code}\n" http://www.example.net
<html><body><h1>It works!</h1>
<p>This is the default web page for this server.</p>
<p>The web server software is running but no content has been added, yet.</p>
</body></html>
200
```

The extra information gets posted at the end of the request. In this case, the HTTP status code is 200, which is what we want. The curl man page (type man curl) lists a number of extra options for the -w argument that you can chain together in your output. Here's an example of how you might