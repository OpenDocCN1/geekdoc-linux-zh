# Client Request

Client HTTP requests come in two basic forms: GET and POST. A GET request is sent to the server when a user types a URL into a browser or clicks a hyperlink. The browser builds an HTTP packet that contains, at minimum, the request method or command type, the name of the object that the user is requesting, the HTTP version, the product name of the browser, and the list of file types that the browser can handle:

```
GET /login HTTP/1.0
User-Agent: Mozilla/4.02 [en] (Win95; I)
Accept: image/gif, image/jpeg, text/html, /*
```

Meanwhile, the domain name (or IP address), the qualifier for the request, and the user input parameter (if any) are passed as what is known as the query string:

```
http://www.mc.com/servlet/login?user=don&pass=secret
```

Again, the "port" of the URL says that it is using the Hypertext Transfer Protocol. The domain name of the server is "http://www.mc.com" (although this could also be an IP address). The "servlet" is the qualifier for the requested object, and "login" is the name of the requested object. The question mark indicates that a query string follows, and the ampersand then shows the start of a new key/value parameter pair. In the example, the parameters are the user name "don," and the password "secret" (which isn't, now).

This brings up (justifiable) concern about sending information such as passwords as free text across the Internet. To avoid this, use POST instead of GET. An HTTP POST request embeds all the parameters to the HTTP packet, instead of sending them as part of the URL. Then, as long as you use Secure Sockets Layer configured on your server, all the data in the HTTP packet is encrypted by the browser and decrypted by the server. Explicitly specifying POST is covered later in this chapter.

# The Response

The earliest Web servers served merely static HTML and images. When a user requests a static HTML page, the qualifier portion of the request is used as the path to the HTML file on the host. For example, if the request was for "http://www.WidgetsRU.com/html/HelloWorld.html", the Web server would simply open the file HelloWorld.html in the directory called, and then stuff the contents of that into an HTTP response packet. That response packet is fairly easy to build, as you can see in Figure 6.1. The packet starts by specifying which version of HTTP it contains (in this case, 1.0), followed by the HTTP status codes. Status codes are used to tell the client (the browser) whether the request was successfully filled. A summary of HTTP status codes is shown in Table 6.1.