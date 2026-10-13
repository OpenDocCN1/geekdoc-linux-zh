# Server API Programming

Modern Web servers such as Apache include application program interfaces (APIs) which allow applications to directly interact with the server. This allows the creation of application development environments that are integrated parts of the Web server and run either as part of the Web server process itself or as a single external process.

When requests are made for applications run through that application development environment, the Web server can simply direct the request to the application engine through the API without starting a new process or launching a command interpreter as required for CGI-BIN. The application can produce dynamic HTML and return it to the browser directly through the Web server’s API rather than sending the data to the standard output and then letting the Web server read it back in from there. The relationship of API-based application development environments with Web servers is illustrated in Figure 25.2.

![](bbox=[0.134, 0.377, 0.63, 0.63])

This direct interaction between the Web server and the application engine allows for more efficient dynamic and interactive Web applications that can generally handle more requests and larger numbers of simultaneous requests than CGI-BIN solutions on the same system. For this reason, API-based solutions are commonly used on interactive and dynamic Web sites today.

In addition to efficiency advantages as compared to CGI-BIN programming, API-based solutions provide the following potential advantages:

+   - Easy access to features of the Web server through the API
+   - Integration with the Web server’s security and authentication mechanisms

However, Web application environments have disadvantages. Most notably, the programming languages of most of these environments are focused on a particular task: obtaining dynamic data and using it to generate HTML for the browser. This focus means the