When you search on the Web, you can use a keyword search or a URL. The URL tells you what machine your information is located on and the path name to the document on that machine. A URL can also contain a protocol that identifies the method you want to use to access the page. Machines on which Web pages live are called *Web servers*. A *Web client* is the machine that requests pages from a server.

# HTTP

The communication between the server and the client requires the use of HTTP. When a client requests a document, it issues an HTTP request to the machine specified in the URL. When the server receives the request, it looks for the page requested by the client. If the server finds the correct page, it responds with the contents of the page. This is called an *HTTP transaction*.

A client machine needs to have a Web browser that can make HTTP requests. Some of the more popular browsers are Microsoft Internet Explorer and Netscape Navigator. Many e-mail programs such as Microsoft Outlook, Qualcomm’s Eudora, and others also can place HTTP requests and process HTML pages. Machines that receive HTTP requests must have a Web server program that understands them.

An HTTP request is a single line of text that provides information to the server about the client, its capabilities, and the page being requested. There are five specific parts to an HTTP request:

+   - Type of request
+   - A general header
+   - A request header
+   - An entity header
+   - The entity body

The first line of the HTTP request is the request type, which tells the server how to retrieve the page the client is requesting. This is a required parameter for all HTTP requests. The other four parts are optional. The general headers can be used to send information to the server detailing the type of connection or the current time. Request headers describe the client and its capabilities. They can also include information about the name of the machine the client is running, the client’s name, and the type of information the client understands. The entity head and body are used to send documents to the server and employ tools that allow you to create and publish Web pages to a server or submit a form.