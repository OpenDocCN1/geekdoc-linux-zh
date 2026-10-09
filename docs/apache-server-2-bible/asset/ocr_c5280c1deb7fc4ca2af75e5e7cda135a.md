+   1. Client system sends a request to the Web server. The Web server determines if the request needs to be serviced by a CGI program or not.

+   2. The Web server creates a new CGI process and the process initializes itself.
+   The Web server passes various request-related information to the program via environment variables. Depending on the request method (GET or POST), the user data is stored in either an environment variable called QUERY_STRING or put in the process's standard input.

+   3. The CGI application performs its tasks and sends all its output to the standard output, which the Web server reads and parses (with the exception of standard nonparsed header applications).

+   4. The CGI program exits and the server returns the CGI output to the client.

+   5. The output of the CGI program is sent to the client system.

FastCGI processes are persistent. After finishing a request, they wait for a new request instead of exiting, as shown in Figure 14-3.

![](bbox=[0.18, 0.45, 0.82, 0.95])

Figure 14-3: The FastCGI request-processing model