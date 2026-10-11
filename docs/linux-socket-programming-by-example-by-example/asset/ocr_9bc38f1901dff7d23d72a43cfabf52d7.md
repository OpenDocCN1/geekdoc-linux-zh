+   3. Create a socket (lines 71 to 73).
+   4. Create the server socket address (lines 78 to 92).
+   5. Bind the socket address (lines 97 to 101).
+   6. Mark the socket as a listening socket (lines 106 to 108).
+   7. Start the client service loop (line 113).
+   8. Accept a client connection (lines 117 to 123).
+   9. Generate a date and time string (lines 128 to 131).
+   10. Write the date and time string back to the client (lines 136 to 138).
+   11. Close the client connection (line 149).

Some steps require a bit of further explanation. In step 2, the program accepts a port number as an optional command-line argument two. This is necessary, because you don't want to run your version of the server on the standard port 13 (remember from the last chapter, your daytime server listens on that port). Instead, you'll use port 9999 by default, which does not require root privileges to run, and it won't disrupt your standard services. The command-line parameter permits you to use different port numbers if you prefer.

> **NOTE**
> 
> TCP/IP ports 1 to 1023 are reserved for privileged programs (running as root). Non-privileged programs use ports 1024 or greater.
> 
> Note also that a port value of zero is a wild port number. An unassigned port number will be assigned when bind(2) is called, if the port number is specified as zero.

Step 4 is different from previous programs. Line 81 has a call to *strcmp(3)* to see if the value `"*"` was given for the server address. If so, then a wild address is provided in lines 90 and 91. Now this might raise your eyebrow, because it was mentioned earlier that server addresses couldn't be completely wild. The important word to notice is "*completely*." The port and IP number cannot both be wild. The port number is not wild in this example, but it is permitted for the IP number to be wild in the server address. This allows the server to accept connections on any IP interface. This becomes important for systems that have several network cards.

> **TIP**
> 
> A server address cannot completely wild. However, you can specify a port number, the IP number portion of a TCP/IP address can be valid (INADDR_ANY). This allows your server to accept connections from any valid IP interface on that host.