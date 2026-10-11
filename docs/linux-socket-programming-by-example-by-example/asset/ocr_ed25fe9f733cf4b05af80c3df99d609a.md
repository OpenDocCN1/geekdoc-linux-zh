# **CAUTION**

Symbolic signal names in commands such as the kill command are being promoted these days. One reason to use these symbolic symbol names is for safety against typing errors. For example, the command \`\`kill -t 313\`\` can be typed as:

```
kill -HUP 313
```

Some users (author included) prefer to live dangerously and have resisted making this change.

The above session accomplishes the following:

+   1. The su command is used to change to the root account.
+   2. Then you find out what the process ID of the inetd daemon is. The ps command indicates in the example that the process ID is 313 for the inetd daemon process (your process ID may be different).
+   3. The kill -t 313 command is used to send the signal SIGHUP to process ID 313 (your process ID may be different). Be sure to not forget the -t (or -HUP) argument on the command line. Otherwise, you'll kill off your inetd daemon!

Having done all of this, you should now be able to repeat the telnet test and verify that it works.

# **The daytime Client Program**

The program shown in Listing 7.7 performs the following simple steps:

+   1. Looks up the daytime service for the tcp protocol.
+   2. Connects to your PC's daytime server, using tcp.
+   3. Reads the server date and time string that it sends back to your socket.
+   4. Reports the data and time string to your terminal session.
+   5. Closes the socket and exits back to the shell.

The client program in Listing 7.7 is presented next.

![](bbox=[0.1, 0.82, 0.18, 0.95])

# **Listing 7.7:** daytime.c—The Client daytime Demo Program

```
1: /* daytime.c:  
2:  *  
3:  * Example daytime client:  
4:  */  
5: #include <stdio.h>  
6: #include <unistd.h>  
7: #include <stdlib.h>
```