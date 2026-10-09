In the case of nonparsed header applications, the CGI application is responsible for producing appropriate HTTP headers, and in all other cases the Web server produces appropriate HTTP headers based on the content type found in the `STDOUT` of the program. The Web server logs any error information that is written to the CGI program's standard error.

The Web server creates FastCGI application processes to handle requests. The processes may be created at startup or on demand. The FastCGI program initializes itself and waits for a new connection from the Web server. Client request processing in a single-threaded FastCGI application proceeds as follows:

+   1.  When a client request comes in, the Web server decides if the connection needs to be handled by a FastCGI program or not.
+   2.  If the request needs to be serviced by a FastCGI program, the Web server then opens a connection to the FastCGI process, which is already running.
+   3.  The server sends the CGI environment variable information and standard input over the connection. The FastCGI process sends the standard output and error information back to the server over the same connection and then the FastCGI process closes the connection.
+   4.  The Web server responds to the client with the data that has been sent by the FastCGI process, completing the request. The FastCGI process then waits for another connection from the Web server.

# Basic architecture of a FastCGI application

As you already know, unlike a CGI program, a FastCGI program keeps running after it processes a request. This allows it to process future requests as soon as they come, and also makes the architecture of the FastCGI program different from a CGI program. A CGI program executes sequentially and exits, whereas a FastCGI program executes sequentially and loops forever. Figure 14-4 shows the basic architecture of a FastCGI application.

As the figure shows, a FastCGI program typically has an initialization code segment and a response loop segment that encapsulates the body of the program. The initialization code is run exactly once, when the application is initialized. Initialization code usually performs time-consuming operations such as opening databases or calculating values for tables.

The response loop runs continuously, waiting for client requests to arrive. The loop starts with a call to `FCGI_Accept`, a routine in the FastCGI library. The `FCGI_Accept` routine blocks program execution until a client requests the FastCGI application. When a client request comes in, `FCGI_Accept` unblocks, runs one iteration of the response loop body, and then blocks again, waiting for another client request. The loop terminates only when the system administrator or the Web server kills the FastCGI application.