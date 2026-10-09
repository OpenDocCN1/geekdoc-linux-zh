![](bbox=[0.17, 0.15, 0.78, 0.45])

Figure 12-1: How a CGI program works.

helloworld.cgi. The Web server launches the application, waits for it to complete, and returns output. Then, it transmits the application’s output to the Web client on the other side.

What happens when you want the client to be capable of interacting with the application? Well, input data from the client must be supplied to the application. Similarly, when an application produces output, how does the server or client know what type of output to return? A program can produce a text message, an HTML form for further interaction, an image, and so on. As you can see, the output can vary a lot from application to application, so there must be a way for applications to inform the Web server and the client about the output type.

CGI defines a set of standard means for the server to pass client input to the external applications, and it also defines how an external application can return output. Any application that adheres to these defined standards can be labeled as a CGI application/program/script. For simplicity, I use the term CGI program to mean anything (such as a Perl script or a C program) that is CGI-specification compliant. In the following section, I discuss how the CGI input/output process works.

# ## CGI Input and Output

There are many ways a Web server can receive information from a client (such as a Web browser). The HTTP protocol defines the way in which a Web server and a client can exchange information. The most common methods of transmitting request data to a Web server are GET requests and POST requests, which I describe in the following sections.