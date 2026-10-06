# Chapter 9: Using the Internet and the Web 363

The second part of a URL takes you to the computer that is hosting the Web content. Web servers begin with www (or sometimes home). However, if you type the correct protocol (usually http), you will be directed to the right service at the host computer. The next piece of this is just the host.domain style of Internet address that is always used with the Internet (as redhat.com, linuxtoys.net, or whitehouse.gov). An optional port number can be racked on the host.domain name. For example, to request the port for HTTP services (port 80) from the host called www.linuxtoys.net, you can type http://www.linuxtoys.net:80.

> TIP: When you need a specific port number to request the service attached to the computer on your request. A port number is like a telephone extension in a big company. A main telephone number (such as the host.domain name) gets you to a switchboard. The extension (like the port number) connects you to the right person (like the service associated with a port).

The third part of a URL identifies the location of the content on the host computer. Sections in a Web page can be identified with a pound sign (#) and an identifier following the Web page location. For example, the craft section of the bsched.htm page at handsonhistory.com would appear as:

```
http://www.handsonhistory.com/bsched.htm@craft
```

The filename extension (such as .htm or .html) further identifies the content type.

# Web pages

If you look at the HTML source code that produces Web pages, you see that it consists of a combination of information and markup tags, all of which are in plain-text format. The idea is to have Web pages very portable and flexible. You can create a Web page with vi, emacs, edit, or any text editor on any computing platform. Alternatively, simplified front-end programs can be used to produce WYSIWY (What You See Is What You Get) interfaces that let you see what you are creating as you go.

HTML tags are set apart by right and left brackets. Tags come in pairs, with a beginning tag, the information, and an ending tag. The beginning tag contains the tag name, while an ending tag contains a forward slash (/) and the tag name. Here is a minimal HTML page:

```
<html>
<head>
<title>Greetings from Wisconsin</title>
</head>
<body>
Here we are in beautiful Madison.
</body>
</html>
```