# 76 · CHAPTER 6

```
HTTP/1.0 200 OK
Server: Little Web Server
Content-type: text/html
Content-length: 133

<html><body>Hello World!</body></body></html>
```

Figure 6.1: An HTTP packet contains header information along with an embedded file, typically HTML, that is the HTTP server's response to the client's request.

# Table 6.1: HTTP Status Codes

| Error | Description |
|---|---|
| 1xx | Informational. HTTP/1.0 does not define any, but HTTP/1.1 does. |
| 2xx | Successful. The request was received, understood, and accepted. |
| 3xx | Redirection. The server requests the Web client redirect to another URL |
| 4xx | Client error. The request was improperly formatted or cannot be fulfilled. |
| 5xx | Server error. There was a valid request that the server cannot fulfill. |

You have noticed that the HTTP response packet in Figure 6.1 contains not the complete contents of the HelloWorld.html file, but also a few lines that further describe the response. Those extra lines contain HTTP headers. The header tells the browser the name of the HTTP server that handled its request. The content type header specifies that the embedded content contains text-based HTML, while the content-length header gives the total length of the file. There are more HTTP headers than server, content type; a few of the more interesting ones are listed in Table 6.2.

# Table 6.2: HTTP Headers that Enable Sophisticated Internet Applications

| Header | Description |
|---|---|
| Allow | Tells the client which HTTP methods are supported, such as get, post, and head. |
| Expires | The date when the HTML becomes invalid. |
| Pragma | A general-purpose field commonly used to specify "no cache". |
| If-Modified-Since | Returns the file to the client only if modified since a date. |
| Last-Modified | The date when the file was last modified. |
| Location | The directory of the server-based file. |
| Referer | The address of the file linked to this file. |
| Set-Cookie | Application-specific information, often used to maintain state across a stateless protocol. |
| User-Agent | The name and version of the HTTP client. |

# Where's My Package?

When the Web first became ubiquitous, every company had to have a Web site. Many of them slapped one together by converting their marketing material to HTML and images. This type of Web is known as brochure because it is nothing more than your standard advertising information, except that it is on the Web. To get a return on their investment in a Web site, however,