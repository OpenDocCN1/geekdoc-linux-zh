# ## 17.5 Lab – two FTP sessions using telnet as client

We’re going to run 2 FTP sessions by hand using **telnet** and **netcat** to illustrate in practice the difference between active and passive modes. We’ll start with passive mode, because it’s easier. In the diagrams we’ve inserted extra lines to show the time sequence in which we entered commands and received replies. Long lines are wrapped. Lines for the second clients are indented a lot. The conversations below illustrate:

+   * the end-user commands that you type to your FTP client’s user interface component (e.g., “put”, “get”, “ls”, “rename”) aren’t what goes over the wire. The on-wire commands are four-character strings, like the SMTP and POP commands we saw earlier. You can get a list of the user commands by connecting to the FTP server and entering **HELP**. (You don’t have to enter username and password first.)
+   
+   * the response codes from the server are like the HTTP response codes, e.g.

| Code | Meaning |
| :--- | :--- |
| 125 | Data connection already open; transfer starting |
| 200 | Command OK |
| 331 | User name OK, need password |
| 421 | Service not available, closing control connection |
| 501 | Syntax error in parameters or arguments |

RFC-959 lists all the response codes and their meanings.

# ### 1. Passive mode

We use two separate **telnet** connections to replicate the actions of an FTP client. The sequence of actions (Figure 17.9) is:

+   a. connect to the FTP server using **telnet**. This is the control connection
+   
+   b. log in to the FTP server, giving the username and password
+   
+   c. send the **PASV** command to tell the server to use passive mode
+   
+   d. **telnet** prints the server’s reply, which is in the format a,b,c,d,p1,p2, where a.b.c.d is the server’s IP address and (p1 x 256 + p2) is the port number it’s going to open for the client – in this example (4 x 256 + 12) = 1036
+   
+   e. leaving **telnet** running in another window or on another terminal, connect another **telnet** session to the server on the port we just calculated, 1036. It sits waiting for the server to connect. This is the data connection
+   
+   f. in **telnet-1**, enter the FTP on-wire command to retrieve the file, “**RETR /tmp/j**”. This is sent over the control connection to the server …
+   
+   g. … which sends the contents of file */tmp/j* to our **telnet-2** over the data connection, and then terminates the connection.